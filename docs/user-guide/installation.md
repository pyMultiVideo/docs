# How to install pyMultiVideo

There are two main steps to installing pyMutliVideo

1. Cloning the repository
2. Running the powershell installation scripts

## Cloning the repository

The recommended way to install this program is to clone this repository using github. If you intend on installing it for all users consider installing it in `C:/Program Files`.

To install using Github: 

1. Install Git Bash if you havent already. 
2. Open the Git Bash powershell
3. Navigate to the folder you would like to install the repository in (e.g. `cd C:/Program Files/`)
4. Clone the repository `git clone https://github.com/pyMultiVideo/code.git`

This allows for an easier [updating](/docs/user-guide/updates.md) process

## powershell files for installation of the application dependancies

To install this application you can run these powershell installation scripts in the following order.

>IMPORTANT: For the installtion to work properly, you must run the installation scripts in the directory that they located (i.e. `/code/_installation`)

  1. [INSTALL_MINICONDA_ADMIN.ps1](https://github.com/pyMultiVideo/code/tree/main/_installation/INSTALL_MINICONDA_ADMIN.ps1)
  2. [INSTALL_PYSPIN.ps1](https://github.com/pyMultiVideo/code/tree/main/_installation/INSTALL_PYSPIN.ps1).  
  3. [INSTALL_FFMPEG.ps1](https://github.com/pyMultiVideo/code/tree/main/_installation/INSTALL_FFMPEG.ps1)


You can check the requirements of the installation were met with the following scripts

  1. [CHECK_SPINNAKER_INSTALLATION.ps1](https://github.com/pyMultiVideo/code/tree/main/_installation/CHECK_SPINNAKER_INSTALLATION.ps1)
  2. [CHECK_FFMPEG_INSTALLATION.ps1](https://github.com/pyMultiVideo/code/tree/main/_installation/CHECK_FFMPEG_INSTALLATION.ps1)

## What the scripts do
*Windows only*

### INSTALL_MINICONDA.ps1

This script installs a virtual environment manager called miniconda. At a high level, a virtual enviroment is a separate installation of python. This is useful for avoiding dependancies conflicts that occur between different python packages that you might want to install. For more information an article is linked [here](https://medium.com/@aminasaeed223/a-comprehensive-tutorial-on-miniconda-creating-virtual-environments-and-setting-up-with-vs-code-f98d22fac8e2).

This is useful here because the pyMultiVideo requires the following: 
1. The latest version of python that the SDK supports is `python==3.10`
2. The SDK does not support numpy version 2 or above.

The script also creates a python 3.10 virtual environment in miniconda and installs the requirements of pyMutliVideo, with the execption of the PySpin API which is installed in `INSTALL_PYSPIN.ps1`

### INSTALL_PYSPIN.ps1

This get the Spinnaker SDK from their [website](https://www.teledynevisionsolutions.com/products/spinnaker-sdk/?model=Spinnaker%20SDK&vertical=machine%20vision&segment=iis), however the script provides a direct download link to the SDK.
*It has only be tested using python 3.10*

This SDK is installed on the computer and the spinnaker python api is also downloaded, and installed into the miniconda virtual environment. 

### INSTALL_FFMPEG

The encoder in this application uses ffmpeg so you need ffmpeg installed (by simply running [this](https://github.com/pyMultiVideo/code/tree/main/_installation/CHECK_FFMPEG_INSTALLATION.ps1) script.) as well as the ffmpeg api ([`pip install ffmpeg-python`](https://pypi.org/project/ffmpeg-python/))


## Opening the application

To open the application you must run the `pyMultiVideo_GUI.pyw` in the conda environment created (`pyMultiCam_env`). You can do this by either by running `conda activate pyMultiCam_env`, the using this version of python to open the GUI file, or you can run the [OPEN_APPLICATION.ps1](https://github.com/pyMultiVideo/code/blob/main/OPEN_APPLICATION.ps1) script which will do this automatically.