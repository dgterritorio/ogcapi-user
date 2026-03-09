# README

This site creates the user documentation (in HTML and pdf) for the OGC API SDI, at DGT. Docs are built using [mkdocs](https://www.mkdocs.org/). *Note: To avoid breaking changes, we must stay on [mkdocs < 2.0](https://squidfunk.github.io/mkdocs-material/blog/2026/02/18/mkdocs-2.0/).*

Build using:

```bash
# build a virtual Python environment in isolation
python3 -m venv .
. bin/activate
git clone https://github.com/dgterritorio/ogcapi-user.git
cd ogcapi-user
# install required dependencies
pip3 install -r requirements.txt
# build step generates a pdf at site/pdf
mkdocs build
mkdocs serve
```

The site will be automatically deployed through a [GitHub action](https://github.com/dgterritorio/ogcapi-user/blob/main/.github/workflows/main.yml).It is live at: https://dgterritorio.github.io/ogcapi-user/

## License

Licensed using [MIT](./LICENSE).
