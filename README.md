# Zammad user documentation

If you want to contribute to the Zammad documentation you can edit the rst files and create pull requests.

We take care about the translation part, so please don't change anything else whithin the repository. These changes would be discarded anyway ;)

## Note:
**Please modify only *.rst files** the *.PO and *.MO files are autogenerated!

## ReStructuredText markup

If you like to edit the docs use the ReStructuredText markup language. Info about this markup language can be found at:

- http://www.sphinx-doc.org/en/stable/rest.html
- http://docs.readthedocs.io/en/latest/_themes/sphinx_rtd_theme/demo_docs/source/demo.html

Thanks! ❤ ❤ ❤

  Zammad Team

[![Documentation Status](https://readthedocs.org/projects/zammad-user-documentation/badge/?version=latest)](https://zammad-user-documentation.readthedocs.io/de/latest/)

## Local tests (mostly internal stuff)

If you want to test the docs for yourself you need a local installation of sphinx and gettext.

```
pip install sphinx sphinx-autobuild sphinx-intl sphinx_rtd_theme

```

### Example for a local HTML build

```
make html
```

### Example workflow for localization using transifex

If you have to work on the translations you need gettext.

For OS X use HomeBrew or build from source. For Linux use your package manager.

```
brew install gettext
```

The workflow itself

# create .tx config
```
tx init
```

# or if you just want to update a ressource
```
tx set --source -r <project_slug.resource_slug> -l <lang> <file>

make clean
```

# this will generate the strings from the *.rst files
```
make gettext
```

# this will generate the locales (DE|EN)
```
sphinx-intl update -p _build/locale/ -l de -l en
```

# this will update the resource files from the pot dir
```
sphinx-intl update-txconfig-resources --pot-dir _build/locale --transifex-project-name zammad-user-documentation
```

# push to transifex (if configured)
```
tx push -s
```

# after translation pull needed languages from transifex
```
tx pull -l en
```

# build the .MO files for use with readthedocs
```
sh build_mo.sh
```

After a successful build, push to this repo and readthedocs will update itself.

# manual language-based build (_build/html/) (for testing)

```
make -e SPHINXOPTS="-D language='de'" html
make -e SPHINXOPTS="-D language='en'" html

```
