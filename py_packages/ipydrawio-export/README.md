# IPyDrawio Export

> PDF export of [drawio](https://www.diagrams.net) diagrams for JupyterLab.

---

[![install from pypi][pypi-badge]][pypi] [![build][workflow-badge]][workflow]
[![coverage][cov-badge]][cov]

[pypi-badge]: https://img.shields.io/pypi/v/ipydrawio-export
[pypi]: https://pypi.org/project/ipydrawio-export
[workflow-badge]:
  https://github.com/deathbeds/ipydrawio/workflows/.github/workflows/ci.yml/badge.svg
[workflow]:
  https://github.com/deathbeds/ipydrawio/actions?query=branch%3Amaster+workflow%3A.github%2Fworkflows%2Fci.yml
[cov-badge]:
  https://codecov.io/gh/deathbeds/ipydrawio/branch/master/graph/badge.svg?token=9B74VKHQDK
[cov]: https://codecov.io/gh/deathbeds/ipydrawio

---

See the [project repo](https://github.com/deathbeds/ipydrawio) for more
information.

## Installation

```bash
pip install ipydrawio-export
```

## Server Extension

`ipydrawio-export` runs as a [server extension][serverext]. When installed, it
_should_ be automatically configured. If problems arise, it can be manually
_enabled_:

```bash
jupyter server extension list   # If you don't see it here...
jupyter server extension enable --sys-prefix --py ipydrawio_export  # run this...
jupyter server extension list   # ... then check it again
```

> Note: If you are starting your server with `jupyter notebook` (not
> `jupyter lab`), the commands above will be `serverextension` instead of
> `server extension`!

## Command-Line Usage

### Exporting PDF

PDF can also be generated from the command line:

```bash
pip install ipydrawio-export
jupyter drawio-export pdf some_file.dio
```

If needed, the `nodejs` application will be installed into the Jupyter data
path.

```bash
jupyter config --paths  # it uses the one in the environment
```

> In the future, it's hoped this can be packaged more conveniently.

### Provisioning

To ensure the `nodejs` application is installed _without_ exporting a PDF (e.g
when building a `docker` container).

```bash
jupyter ipydrawio-export provision
```

### Provision locations

If defined, these environment variables will be respected, and an
`ipydrawio_export` folder will be created:

- `$JUPYTER_DATA_DIR`
- `$IPYDRAWIO_DATA_DIR`

Otherwise, `ipydrawio-export` will provision its files into
`{sys.prefix}/ipydrawio_export`.

Of note:

- access to the internet is required
- this location must be writeable by the user
- there must be about 400MiB available, primarily for `puppeteer`'s `chromium`

## Open Source

This work is licensed under the [Apache-2.0] License.

The vendored code from [@jgraph/draw-image-export2][] is also licensed under the
[Apache-2.0][draw2-license] License.

[@jgraph/draw-image-export2]: https://github.com/jgraph/draw-image-export2
[apache-2.0]:
  https://github.com/deathbeds/ipydrawio/blob/master/py_packages/ipydrawio-export/LICENSE.txt
[draw2-license]:
  https://github.com/jgraph/draw-image-export2/blob/master/LICENSE
[serverext]:
  https://jupyter-notebook.readthedocs.io/en/stable/examples/Notebook/Distributing%20Jupyter%20Extensions%20as%20Python%20Packages.html