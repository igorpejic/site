---
author: "Igor Pejic"
date: 2024-05-17
linktitle: "Django InterfaceError: Connection already closed"
title: "Django InterfaceError: Connection already closed"
weight: 10
---
## Background

*Stack: gunicorn + Django + pyscopg2*

Error `InterfaceError: Connection already closed` started appearing after performing new deploys of the application.
These errors would appear from multiple gunicorn workers at the same time some 60 seconds after the workers would initialize.

## Understanding the stacktrace

The error indicates that when Django ORM attempted to perform an SQL query through an open Psycopg2 connection, the connection was already closed. Django tries to execute the query through the assumed open connection, but when it is closed, the error occurs.
After the closing of the connection is discovered, Django creates new connections for each worker and the error does not appear anymore.

## Root Cause Analysis

The key intuition is to understand why and who is closing the database connection.

After some digging, the issue was traced to the combination of how gunicorn application loading was configured and a database interaction during `AppConfig.ready`.

Gunicorn applicaiton is configured to use [`preload_app`](https://docs.gunicorn.org/en/stable/settings.html#preload-app)
 to eagerly load the application to save on RAM.


In addition, in [`AppConfig.ready`](https://docs.djangoproject.com/en/5.0/ref/applications/#django.apps.AppConfig.ready), there is a `doing_db_stuff_method()`, which is interacting with the database connection using Django ORM.

```python
class MyAppConfig(AppConfig):
    name = 'my_app'

    def ready(self):
        doing_db_stuff_method()
```

AppConfig gets called during app import time (pre-fork in gunicorn). Since interaction with the database happens before the gunicorn process gets forked, the database connection gets reused in multiple gunicorn workers.
After, when one worker closes that connection, all other workers suffer from it as they have been using this identical connection.
This happens because of the way `preload_app` forking essentially copies memory across workers.


## Solutions

This leaves us with 2 viable solutions:

- **Stop using `preload_app` in gunicorn.** In this case the `AppConfig` loading would happen after workers get forked so the problem is avoided. However, this also means each worker will load the application on their own, so a larger RAM usage is expected.

- **Do not interact with the database during `AppConfig` app loading.** Alternatively, perform this in an async job, migration or other way suited for your use-case.

## Key Takeaways

1. **Be careful with Database Operations in `AppConfig.ready`**: Where possible, avoid database interactions in the AppConfig.ready method to prevent connection issues during the forking process.

2. **Understand Gunicorn Configuration Implications**: Be aware of the implications of Gunicorn's preload_app setting on database connections. Ensure configurations align with your application's architecture and deployment strategies.
If you can, avoid performing database operations in `AppConfig.ready` method.
