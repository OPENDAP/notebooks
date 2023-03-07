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

## Geospatial data subsetting without regridding
Added 9/24/21

Subsetting level 2 satellite data generally requires regridding. However, using STARE and
Hyrax server-side function, these data can be subset without first regridding them. See
[Subsetting Level 2 Data without Regridding](https://github.com/OPENDAP/notebooks/blob/master/stare/STARE_Subsetting_Using_lat_lon.ipynb)
for a notebook that demonstrates these new features that are the result of a NASA ACCESS
grant in collaboration with Rilee, Inc., Bayesics, Inc., and UCSB.

## Geospatial data subsetting
The first notebook illustrates subsetting regularly gridded data (i.e., NASA's Processing
Level 3) using Latitude and Longitude values instead of raw array indices.

* [Geospatial subsetting using server functions](https://github.com/OPENDAP/notebooks/blob/master/Geospatial_subsetting_using_server_functions.ipynb)

## STARE Index plotting
This notebook reads from STARE index 'sidecar' files and plots the indices. See the README
in the `stare` subdirectory for information about setting up the environment. There is an
`environment.ymp` file but you will need to add some things not currently in `conda` or `pip`.

* [STARE]()

## What's needed to run these
To develop these notebooks, we use Anaconda to establish a local package management
environment. Get and install Anaconda. All our work uses Python 3. Jupyter notebooks
often make use of obscure Python packages. Instead of listing them here, we'll include
comments in the notebooks themselves regarding how those packages were installed
in the Anaconda environment.

### Anaconda tricks - for OPeNDAP develoeprs
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

To use the environment.yml file to make an environment with the packages needed
to run the notebooks, use `conda env create -f environment.yml`. The general form of this 
command is `conda env create -n conda-env -f /path/to/environment.yml`. The `conda ...` 
command can also update an existing environment using the packages in a yml file with 
`conda env update -n conda-env -f /path/to/environment.yml`.

See 
[Managing environments](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)
for more information about managing environments with `conda`.

### Jupyter and conda
While an `environment.yml` file does not need to mention jupyter to work with Binder, to get `conda`
to build an environment that includes jupyter notebook support, I added `ipykernel` to the `environment.yml` 
file. However, I didn't test that; it's a hunch based on my running two commands:
1. `conda install -n opendap ipykernel` # the environment name is 'opendap'
2. `python -m ipykernel install --user --name "opendap" --display-name "Python (opendap)"`

#### My Experience OS-X 13.2.1 02/28/2023 - ndp
I did the above but nothing seemed to work. Strange error messages from `jupyter` 
when I try to start the notebook. I checked on the jupyter version and I saw this:
```shell
(opendap) [-bash: ~] jupyter  --version
Selected Jupyter core packages...
IPython          : 8.10.0
ipykernel        : 6.19.2
ipywidgets       : not installed
jupyter_client   : 7.4.9
jupyter_core     : 5.2.0
jupyter_server   : not installed
jupyterlab       : not installed
nbclient         : not installed
nbconvert        : not installed
nbformat         : not installed
notebook         : not installed
qtconsole        : not installed
traitlets        : 5.7.1
```
So I tried installing each missing thing, and then re-checking the version. Some things, 
like `ipywidgets` installed a bunch of the other missing pieces.
```shell
(opendap) [-bash: ~] conda install ipywidgets
(opendap) [-bash: ~] jupyter  --version
Selected Jupyter core packages...
IPython          : 8.10.0
ipykernel        : 6.19.2
ipywidgets       : 7.6.5
jupyter_client   : 7.4.9
jupyter_core     : 5.2.0
jupyter_server   : 1.23.4
jupyterlab       : not installed
nbclient         : 0.5.13
nbconvert        : 6.4.4
nbformat         : 5.7.0
notebook         : 6.5.2
qtconsole        : not installed
traitlets        : 5.7.1
(opendap) [-bash: ~] conda install jupyterlab
(opendap) [-bash: ~] jupyter  --version
Selected Jupyter core packages...
IPython          : 8.10.0
ipykernel        : 6.19.2
ipywidgets       : 7.6.5
jupyter_client   : 7.4.9
jupyter_core     : 5.2.0
jupyter_server   : 1.23.4
jupyterlab       : 3.5.3
nbclient         : 0.5.13
nbconvert        : 6.4.4
nbformat         : 5.7.0
notebook         : 6.5.2
qtconsole        : not installed
traitlets        : 5.7.1
(opendap) [-bash: ~] conda install qtconsole
(opendap) [-bash: ~] 
(opendap) [-bash: ~] jupyter  --version
Selected Jupyter core packages...
IPython          : 8.10.0
ipykernel        : 6.19.2
ipywidgets       : 7.6.5
jupyter_client   : 7.4.9
jupyter_core     : 5.2.0
jupyter_server   : 1.23.4
jupyterlab       : 3.5.3
nbclient         : 0.5.13
nbconvert        : 6.4.4
nbformat         : 5.7.0
notebook         : 6.5.2
qtconsole        : 5.4.0
traitlets        : 5.7.1
(opendap) [-bash: ~/OPeNDAP/hyrax/notebooks] 
```
And then everything worked! 


### Conda environment management
* [Guide to Conda Environments](https://towardsdatascience.com/a-guide-to-conda-environments-bc6180fc533)
* [Managing environments](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)

## Starting the notebooks
Once you have gotten everything installed (see previous section) you run the 
notebooks from the command line like this:

```bash
jupyter notebook Geospatial_subsetting_using_server_functions.ipynb
jupyter notebook tutorials/pydap_dap2_basic.ipynb
```

## Useful documentation
Here are resources we've found useful in building these notebooks:
* [Advanced Jupyter Notebook Tricks — Part I](https://blog.dominodatalab.com/lesser-known-ways-of-using-notebooks/): Various magic codes like %time
* [Requests](https://requests.readthedocs.io/en/master/user/quickstart/): An HTTP/S request package
* [Basemap](https://basemaptutorial.readthedocs.io/en/latest/): A tool for drawing georeferenced maps.
* [PyDAP](https://www.pydap.org/en/latest/client.html): A flexible tool for accessing data from OPeNDAP servers.
* [matplotlib](https://matplotlib.org/3.2.1/contents.html): The plotter of choice for many.
* [matplotlib basemap](https://matplotlib.org/basemap/index.html): Soon to be deprecated for several years now...
* [Cartopy in Pypi](https://pypi.org/project/Cartopy/)
* [Cartopy](https://scitools.org.uk/cartopy/docs/latest/): The successor to Basemap.
* [Cartopy Basics](https://scitools.org.uk/cartopy/docs/v0.15/matplotlib/intro.html)
* [Cartopy more...](https://scitools.org.uk/cartopy/docs/v0.15/matplotlib/advanced_plotting.html)
* [Markdown for notebooks](https://medium.com/ibm-data-science-experience/markdown-for-jupyter-notebooks-cheatsheet-386c05aeebed): Just in case you need a primer..
* [Binder](https://mybinder.org/) Documentation is at the bottom of the page.
* [H5Py](http://docs.h5py.org/en/stable/quick.html)

Collections of Jupyter notebooks that also demonstrate OPeNDAP. There are many others, but these will get you
started with access patterns that don't use server functions:
* [CloudyDAP notebooks](https://github.com/OPENDAP/cloudydap/tree/master/python): Written by Joe Lee from The HDF Group.
* [PyDAP Examples](https://github.com/betodealmeida/notebooks): Written by Beto DiAlmeida, author of PyDAP.

