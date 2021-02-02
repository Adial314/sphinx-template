# Sphinx Template

This project provides a template for quickly deploying Sphinx documentation websites. The goal is to complete most of the configuration for you so that you can quickly go from nowhere to writing wiki entries as quickly as possible. To this end, this 


## Table of Contents
- [Background](#background)
- [Usage](#usage)


## [Background](#table-of-contents)

Sphinx is an open-source static site generator (SSG) commonly used by developers to serve documentation surrounding the use and development of their project(s). While the wiki entries rely on Markdown notation, Sphinx offers extended functionality when compared against other SSGs like ReadTheDocs with the MkDocs engine.


## [Usage](#table-of-contents)

To use the existing `/project/` folder, skip step 5 and proceed to step 6.

1. Clone this repository and nagivate into it.

2. Delete the .git directory and initialize a new git project for your docs.
```BASH
rm -rf .git
git init
```

3. Create and activate a new Anaconda environment for your project.
```BASH
conda create -n sphinx --python=3.8
conda activate sphinx
```

4. Install the prerequisite software and check the Sphinx version.
```BASH
pip3 install -r requirements.txt
```

5. (optional) Delete the existing `/project/` folder and initialize a new Sphinx project in an empty `/project`. This action will also destroy the configuration of the pre-existing Sphinx project, make sure you understand how the template works and copy any necessary information before creating your own project. The `sphinx-quickstart` command will prompt you for a project name, this name will appear in multiple places and is best named correctly at the start of the project build.
```BASH
rm -rf project
mkdir project
sphinx-quickstart
```

6. Within the `/project/` folder, you should now see the following files and folders:
	* `build/` - stores the static-site output for hosting.
	* `make.bat` - helper for Makefile
	* `Makefile` - contains a set of recipes for building the site
	* `source/` - contains the docs entries and data
		* `conf.py` - configuration details for the Sphinx site
		* `index.rst` - welcome page and table of contents definition

7. Sphinx uses ReStructuredText by default which is too limited for our needs. The `recommonmark` package was already included as a required package in `/requirements.txt`. Following the [Sphinx docs for Markdown](https://www.sphinx-doc.org/en/master/usage/markdown.html), edit the `/ptoject/source/conf.py` file to include the following:

```PYTHON
extensions = ['recommonmark']

...

# -- Other Configurations ----------------------------------------------------

# Force Sphinx to recognize *.rst files as ReStructuredText
# Force Sphinx to recognize *.md files as Markdown
# Expand definition of Markdown to include *.txt files
source_suffix = {
    '.rst': 'restructuredtext',
    '.txt': 'markdown',
    '.md': 'markdown',
}
```

Visit the [ReCommonMark docs](https://recommonmark.readthedocs.io/en/latest/index.html) for more information on configuring this package.
More information on the Sphinx `conf.py` file can be found in the [Sphinx Configuration](https://www.sphinx-doc.org/en/master/usage/configuration.html#confval-extensions) docs page.
Note that [LaTeX support](https://www.sphinx-doc.org/en/master/usage/configuration.html#options-for-latex-output) is present in Sphinx but uses pdflatex instead of the standard HTML builder.

8. Within the `/project/source/conf.py` file, select the HTML theme for the site from the [Sphinx HTML themes](https://www.sphinx-doc.org/en/master/usage/theming.html#builtin-themes). More themes can be found and previewed at [sphinx-themes.org](https://sphinx-themes.org/) where the `conf.py` files can be viewed for free.

9. Add content in the form of either ReStructuredText files (`*.rst`) or as Markdown files (`*.md` and `*.txt`) under the `/project/source/` directory.

10. When you are ready to build the site, run the following commands from the `/project/` folder:

```BASH
make html
```

11. If no error messages have ocurred, then your site has been built in the `/project/build/` directory. Host the site by running the following command from the `/project/build/html` folder. This command will host the static webpages on a local webserver.

```BASH
python3 -m http.server
```

12. Connect to `localhost:8000` in a browser to see your locally hosted docs.


*Written by Austin Dial. Maintained by Seaborn.*
