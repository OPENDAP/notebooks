[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/OPENDAP/notebooks/master)
# Hyrax server functions
This repository holds a collection of Jupyter notebooks that demonstrate how to
use Server functions, an often overlooked feature of the Hyrax data server, to
perform different kinds of processing and subsetting operations on data _before_
they leave a server.

Run these notebooks using [Binder](https://mybinder.org/v2/gh/OPENDAP/notebooks/master).

This project was started at part of the ESDIS PI 20.1 hackfest. If you're reading this
from the [NASA ECC BitBucket repository](https://git.earthdata.nasa.gov/scm/hyrax/notebooks.git), please checkout the [OPeNDAP GitHub repo](https://github.com/OPENDAP/notebooks.git)
of the same name since it may have more notebooks illustrating more functions.

## Geospatial data subsetting
The first notebook illustrates subsetting regularly gridded data (i.e., NASA's Processing
Level 3) using Latitude and Longitude values instead of raw array indices.

* [Geospatial subsetting using server functions](https://github.com/OPENDAP/notebooks/Geospatial%20subsetting%20using%20server%20functions.ipynb)

## What's needed to run these
To develop these notebooks, we use Anaconda to establish a local package management
environment. Get and install Anaconda. All our work uses Python 3. Jupyter notebooks
often make use of obscure Python packages. Instead of listing them here, we'll include
comments in the notebooks themselves regarding how those packages were installed
in the Anaconda environment.

### Anaconda tricks 
Anaconda modifies `.bash_profile` when it installs
an will set any shell to use the anaconda base environment by default,
modifying PATH to use its packages in preference to anything else (and
this breaks our builds as of 4/2020). To disable this, edit the
.bash_profile file, removing the code added by the installer at the
bottom of the file (it's easy to spot) and add a function to enable
the anaconda PATH modification. Here's an example:

```bash
function conda-on() {
    source ~/opt/anaconda3/etc/profile.d/conda.sh
    conda activate base
}
```

To turn on Anaconda, just run `conda-on`

## Useful documentation
Here are resources we've found useful in building these notebooks:
* [Requests](https://requests.readthedocs.io/en/master/user/quickstart/): An HTTP/S request package
* [Basemap](https://basemaptutorial.readthedocs.io/en/latest/): A tool for drawing georeferenced maps.
* [PyDAP](https://www.pydap.org/en/latest/client.html): A flexible tool for accessing data from OPeNDAP servers.
* [matplotlib](https://matplotlib.org/3.2.1/contents.html): The plotter of choice for many.
* [matplotlib basemap](https://matplotlib.org/basemap/index.html): Soon to be deprecated for several years now...
* [Cartopy](https://scitools.org.uk/cartopy/docs/latest/): The successor to Basemap.
* [Markdown for notebooks](https://medium.com/ibm-data-science-experience/markdown-for-jupyter-notebooks-cheatsheet-386c05aeebed): Just in case you need a primer..

Collections of Jupyter notebooks that also demonstrate OPeNDAP. There are many others, but these will get you
started with access patterns that don't use server functions:
* [CloudyDAP notebooks](https://github.com/OPENDAP/cloudydap/tree/master/python): Written by Joe Lee from The HDF Group.
* [PyDAP Examples](https://github.com/betodealmeida/notebooks): Written by Beto DiAlmeida, author of PyDAP.

