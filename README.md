# Igor Pejic's Blog

This is the source code for my personal blog and portfolio website, built with Hugo and the Archie theme.

## Setup

This site works with Hugo v0.113 or later.

### Running the server

To run the development server:

```bash
hugo server --config config.toml
```

### Deployment

To deploy the site:

1. Run the `deploy.sh` script
2. The built code will be available at igorpejic.github.io

### New machine setup

If cloning on a new machine:

```bash
rm -rf public
git submodule init
git submodule update
```

## Directory Structure

```
├── archetypes
│   └── default.md
├── assets
│   └── css
├── config.toml
├── content
│   ├── about.md
│   ├── contact.md
│   ├── _index.md
│   ├── menu
│   └── posts
├── data
│   └── static
├── deploy.sh
├── go.mod
├── go.sum
├── layouts
│   └── partials
├── public
├── README.md
├── resources
│   └── _gen
├── static
└── themes
    └── archie
```

## Theme

This blog uses the [Archie theme](https://github.com/athul/archie) for Hugo. Archie is a minimal and clean theme with a markdown-ish UI.

## License

The content of this project itself is licensed under the [Creative Commons Attribution 4.0 International license](https://creativecommons.org/licenses/by/4.0/), and the underlying source code used to format and display that content is licensed under the [MIT license](LICENSE.md).
