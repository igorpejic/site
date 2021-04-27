Works with Hugo v0.80.0/extended installed with: `sudo snap install hugo --chanell=extended`

Run server:

```
hugo server --theme book --config config.yaml
```

Deploy:

see: deploy.sh

If cloning on new machine:

```
rm public
git submodule init
git submodule update
```
