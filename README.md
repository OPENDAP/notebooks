
# Hyrax server functions
This repository holds a collection of Jupyter notebooks that demonstrate how to
use Server functions, an often overlooked feature of the Hyrax data server, to
perform different kinds of processing and subsetting operations on data _before_
they leave a server.

This project was started at part of the ESDIS PI 20.1 hackfest. If you're reading this
from the [NASA ECC BitBucket repository](https://git.earthdata.nasa.gov/scm/hyrax/notebooks.git), please checkout the [OPeNDAP GitHub repo](https://github.com/OPENDAP/notebooks.git)
of the same name since it may have more notebooks illustrating more functions.

## What's needed to run these
To develop these notebooks, we use Anaconda to establish a local package management
environment. Get and install Anaconda. All our work uses Python 3. Jupyter notebooks
often make use of obscure Python packages. Instead of listing them here, we'll include
comments in the notebooks themselves regarding how those packages were installed
in the Anaconda environment.

## Geospatial data subsetting
The first notebook illustrates subsetting regularly gridded data (i.e., NASA's Processing
Level 3) using Latitude and Longitude values instead of raw array indices.

[Geospatial subsetting using server functions](Geospatial subsetting using server functions.ipynb)
