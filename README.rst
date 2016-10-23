pipreq
======

***THIS PROJECT IS NOW DEFUNCT!***

Please use pipwrap instead: https://pypi.python.org/pypi/pipwrap

|Build Status| |Coverage Status| |PyPI Version| |Supported Python Versions| |Downloads|

pipreq simplifies handling Python project requirements across multiple
environments. pip freeze > requirements.txt gets your project started,
but do you really want mock, coverage, etc. installed on your production
server? Maybe you want to upgrade all your test requirements, but not your
production requirements. If you've ever found yourself sifting through the
output of pip freeze trying to figure out what packages you've installed
but didn't yet add to one of your requirements files, then pipreq is the
tool for you.

Features
--------

-  Inspect a list of packages and create or update a requirements rc file
-  Generate a set of requirements files from an rc file
-  Upgrade all specified packages to the latest versions
-  Remove stray packages in virtualenv

Installation
------------

You can get pipreq from PyPI with:

::

    pip install pipreq

The development version can be installed with:

::

    pip install -e git://github.com/jessamynsmith/pipreq.git#egg=pipreq

If you are developing locally, your version can be installed from the
working directory with:

::

    python setup.py.install

Usage
-----

pipreq uses an rc file to track requirements. You create a section for
each requirements file, and (if desired) select one section to be
shared. The default configuration is as follows:

::

    # .requirementsrc
    [metadata]
    shared = common

    [common]

    [development]

    [production]

This would result in the following requirements directory structure:

::

    requirements/
        common.txt
        development.txt
        production.txt

where development.txt and production.txt both include the line "-r
common.txt"

**Getting Started with pipreq**

1. (Optional) Create an empty .requirementsrc file with your desired
   metadata and sections

2. Interactively populate .requirementsrc file from currently installed
   packages:

   pip freeze \| pipreq -c

3. Generate requirements files from .requirementsrc file:

   pipreq -g

4. Create a top-level requirements.txt file that points to your
   production requirements, e.g. "-r production.txt"

**Keeping requirements up to date with pipreq**

1. Interactively update .requirementsrc file from currently installed
   packages:

   pip freeze \| pipreq -c

2. Re-generate requirements files from .requirementsrc file:

   pipreq -g

3. Upgrade all packages to latest available versions:

   cat requirements/development.txt | pipreq -U

3. Remove stray packages in virtualenv:

   cat requirements/\*.txt | pipreq -x

Development
-----------

Fork the project on github and git clone your fork, e.g.:

::

    git clone https://github.com/<username>/pipreq.git

Create a virtualenv and install dependencies:

::

    mkvirtualenv pipreq
    pip install -r requirements/package.txt -r requirements/test.txt

Run tests with coverage (should be 99%) and check code style:

::

    coverage run -m nose
    coverage report -m
    flake8

Verify all supported Python versions:

::

    pip install tox
    tox

Install your local copy:

::

    python setup.py.install

.. |Build Status| image:: https://img.shields.io/circleci/project/github/jessamynsmith/pipreq.svg
   :target: https://circleci.com/gh/jessamynsmith/pipreq
   :alt: Build status
.. |Coverage Status| image:: https://img.shields.io/coveralls/jessamynsmith/pipreq.svg
   :target: https://coveralls.io/r/jessamynsmith/pipreq?branch=master
   :alt: Coverage status
.. |PyPI Version| image:: https://img.shields.io/pypi/v/pipreq.svg
   :target: https://pypi.python.org/pypi/pipreq
   :alt: Latest PyPI version
.. |Supported Python Versions| image:: https://img.shields.io/pypi/pyversions/pipreq.svg
   :target: https://pypi.python.org/pypi/pipreq
   :alt: Supported Python versions
.. |Downloads| image:: https://img.shields.io/pypi/dm/pipreq.svg
   :target: https://pypi.python.org/pypi/pipreq
   :alt: Number of PyPI downloads
