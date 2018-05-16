# Hello Sphinx

## Install

```sh
$ pip install sphinx recommonmark sphinx_rtd_theme sphinx-autobuild nbsphinx sphinx_fontawesome
```

## Setting
```sh
$ sphinx-quickstart
```

and add following text to `conf.py`

```py
import sphinx_fontawesome
extensions = [
    'nbsphinx',
    'sphinx.ext.mathjax',
    'sphinx_fontawesome',
]

source_suffix = ['.rst', '.md']

exclude_patterns = ['_build', '**.ipynb_checkpoints']

import sphinx_rtd_theme

html_theme = "sphinx_rtd_theme"

html_theme_path = [sphinx_rtd_theme.get_html_theme_path()]

from recommonmark.parser import CommonMarkParser

source_parsers = {
    '.md': CommonMarkParser,
}

from recommonmark.transform import AutoStructify

github_doc_root = 'https://github.com/rtfd/recommonmark/tree/master/doc/'
def setup(app):
    app.add_config_value('recommonmark_config', {
            'url_resolver': lambda url: github_doc_root + url,
            'auto_toc_tree_section': 'Contents',
            }, True)
    app.add_transform(AutoStructify)
```

### Build
```sh
$ make html
```

enjoy!

## Auto build
To build html automatically, add following text to `Makefile`

```makefile
livehtml:
	sphinx-autobuild -b html $(SOURCEDIR) $(BUILDDIR)/html
```

and command `make livehtml`
