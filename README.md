### See this documentation at:

- English: https://dojotdocs.readthedocs.io/
- Portuguese: https://dojotdocs.readthedocs.io/pt_BR/latest/

# dojot documentation

This repository contains the high-level documentation for dojot iot platform.
For specific information regarding each of the sub-components that comprise the solution,
please check the component's own documentation page.

## Build

The readable version of this documentation can be generated by means of sphinx. In order to
do so, please follow the steps below. Those are actually based off
[Read The Docs own documentation](https://docs.readthedocs.io/en/latest/getting_started.html).

### Configuring Pipenv

In order to isolate the environment, it is better to use Python's virtual environments. Even better
than using `virtualenv` by itself, we can use `pipenv`.

Make sure you have Python 3 and its correspondent version of pip installed. Then, install `pipenv`:

```shell
pip3 install pipenv
```

Install the environment:

```shell
pipenv --python 3.8
```

Install the dependencies via `pipenv`:

```shell
pipenv install
```

Enter in the virtual environment:
```shell
pipenv shell
```

Check the [pipenv repository](https://github.com/pypa/pipenv/) for more commands and details.

### **Generating the documentation**

Now you can simply run:

```shell
make html
```

To build the documentation in Brazilian Portuguese language, run the following extra commands:

```shell
sphinx-intl -c source/conf.py build -d source/locale
make html BUILDDIR=build/html-pt_BR O='-d build/doctrees/ -D language=pt_BR'
```

## Update workflow

To update the documentation, follow the steps below:

1. Update the source files for the english version.
2. Extract translatable messages from the english version:

```shell
make gettext
```

3. Update the message catalog (PO Files) for pt_BR language:

```shell
sphinx-intl -c source/conf.py update -p build/gettext -l pt_BR
```

4. Translate the messages in the pt_BR `.po` files. You don't need to deal with these files directly
in your text editor, check the next section for more details.

This workflow is based on the [internationalization feature of Sphinx](http://www.sphinx-doc.org/en/stable/intl.html).

## Useful tools

`.po` files are kinda annoying to handle. Luckily, there are tools that can understand this format
and provide us a better interface to deal with them. Supposing you are using Ubuntu, you can install
`poedit`:

```shell
apt-get install poedit
```

After running it, you can add the catalog to see all your files in its interface in the
`Catalog Manager` under the `File` menu.
