#### Getting Started with Python Package Distribution

**module** is a file containing Python definitions and statements

**packages** are a way of structuring Python module's (need to include a file with __init__.py)


getting started 

1. `pip install -U pip setuptools` 
	- (confirm latest version of pip)
2. `pip install -U twine`
3. python setup.py sdist 
 - creating source distirbution)
4. `python setup.py bdist_wheel`
 - creates .whl file, wheels can be universal or Python version specific.
 - `Wheel. A built-package format for Python. A wheel is a ZIP-format archive with a specially formatted filename and the .whl extension. It is designed to contain all the files for a PEP 376 compatible install in a way that is very close to the on-disk format.`
 
 
Upload Package to [PyPl](https://pypi.org/) (or TestPyPl since the former is a production packaging site)
 
`twine upload --repository-url https://test.pypi.org/legacy/dist/*`

Need to create an account in order to upload packages to PyPi
`sudo pip install --index-url https://test.pypi.org/simple/ spincare-lib`

Packages can be added to GitHub (or other package repositories) instead of PyPl

Package Files

required files:

- setup.py

optional files:

- setup.cfg
- README.rst
- MANIFEST.in
- LICENSE.txt	

Setup.py components

In Setup.py you can tell setuptools to install_requires=[]. The alternative is to include a requirements.txt where the person who wants to use your package will have to pip install requirements.txt manually.

classifiers=[] is the meta data of a project to give people information about if your project is in production/development, the intended audience, license, programming language, natural language, etc.

Can include keywords to describe your package.

Version of project needs to iterate every single time you publish to a python packaging site. 

__init__.py is a good place to put a version. Do not put it in __init__.py AND the setup.py file as that is not DRY and there may be a conflict in the information if you do not remember to update in both places.

Random: Underscores get replaced in online packages with dashes 

Some people package Python packages in eggs although the preferred method has switched to wheels.
