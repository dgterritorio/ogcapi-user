# README

This site creates the user documentation for the OGC API SDI, at DGT. Docs are built using [mkdocs](https://www.mkdocs.org/).

Build using:

`mkdocs serve `

Deploy using

`mkdocs gh-deploy`

The site is live at: https://dgterritorio.github.io/

## Export PDF

Install `with-pdf` plugin:

`pip install mkdocs-with-pdf`

Build:

`mkdocs build`

PDF is generated at `site/pdf/`.


## License

Licensed using [MIT](./LICENSE).
