Heroku buildpack: Python (with scipy)
=====================================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for Python apps, powered by [pip](http://www.pip-installer.org/).

It is a conversion of a [Heroku buildpack](https://github.com/wyn/heroku-buildpack-python) that includes pre-built binaries of numpy and scipy.  Further information can be made on this [StackOverflow answer.](http://stackoverflow.com/a/18948411/1039947)

[![Build Status](https://secure.travis-ci.org/heroku/heroku-buildpack-python.png?branch=master)](http://travis-ci.org/heroku/heroku-buildpack-python)

Usage
-----

Example usage:

    $ ls
    app.py  Procfile  README.md  requirements.txt

    $ heroku create --stack cedar --buildpack git://github.com/kmp1/heroku-buildpack-python.git

    $ git push heroku master
    ...
    -----> Fetching custom git buildpack... done
    -----> Python app detected
    -----> No runtime.txt provided; assuming python-2.7.4.
    -----> Preparing Python runtime (python-2.7.4)
    -----> Installing Distribute (0.6.36)
    -----> Installing Pip (1.3.1)
    -----> Noticed numpy/scipy/scikit-learn. Bootstrapping prebuilt binaries.
    Initialized empty Git repository in /app/.heroku/npscipy-binaries/.git/
    -----> Creating/downloading binaries.
    -----> heroku contents: npscipy-binaries
    python
    python-version
    vendor
    -----> heroku binaries contents: npscipy.tar.gz
    ------> Looking for package numpy in ../requirements.txt
    -----> Creating/downloading numpy-1.7.0.
    -----> Completed Creating/downloading numpy-1.7.0 by unzipping npscipy-binaries/numpy-1.7.0.tar.gz.
    ------> Looking for package scipy in ../requirements.txt
    -----> Creating/downloading scipy-0.11.0.
    -----> Completed Creating/downloading scipy-0.11.0 by unzipping npscipy-binaries/scipy-0.11.0.tar.gz.
    ------> Looking for package sklearn in ../requirements.txt
    -----> Installing dependencies using Pip (1.3.1)
    ...
           Cleaning up...

You can also add it to upcoming builds of an existing application:

    $ heroku config:add BUILDPACK_URL=git://github.com/kmp1/heroku-buildpack-python.git

The buildpack will detect your app as Python if it has the file `requirements.txt` in the root. 

It will use Pip to install your dependencies, vendoring a copy of the Python runtime into your slug. 

Specify a Runtime
-----------------

You can also provide arbitrary releases Python with a `runtime.txt` file.

    $ cat runtime.txt
    python-3.3.0
    
Runtime options include:

- python-2.7.4
- python-3.3.1
- pypy-1.9 (experimental)
