# Igor Pejic's Blog

This is the source code for my personal blog and portfolio website, built with Hugo and the Archie theme.

## Setup

This site works with Hugo v0.113 or later.

### Running the server

To run the development server:

```bash
hugo server --theme archie
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
.
├── archetypes
│   └── default.md
├── config.yaml
├── content
│   ├── _index.md
│   ├── about.md
│   ├── contact.md
│   ├── online_presence.md
│   └── posts
├── data
│   └── static
├── deploy.sh
├── static
│   └── images
├── themes
│   └── archie
└── README.md
```

## Theme

This blog uses the [Archie theme](https://github.com/athul/archie) for Hugo. Archie is a minimal and clean theme with a markdown-ish UI.

## License

The content of this project itself is licensed under the [Creative Commons Attribution 4.0 International license](https://creativecommons.org/licenses/by/4.0/), and the underlying source code used to format and display that content is licensed under the [MIT license](LICENSE.md).
