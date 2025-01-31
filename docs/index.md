## Introducing pyMultiVideo 

>**Open source, Python based, Multiple video acquisition.**

*Key Features*

- `pyMultiVideo` is an application for aquiring images from mulitple cameras simulaneously. This is primarily a scientific application.
- This is a `python 3.10` implementation with GUI written using the [QT framework](https://www.qt.io/product/framework) and has a built-in GUI to see the videos you are aquiring real-time.
- Use of the spinnaker-python API is a key feature of this application. 

### Recommended Usage

pyMultiVideo's usage / recommended usage

### Currently Supported Cameras

PySpin Spinnaker Camera

Tested on:

- `Blackfly` 
- `Pointgrey`

## Getting started

See [here](/user-guide/installation.md) for instructions on how to install this application.

### Dependencies

pyMultiVideo has the following dependencies

- python 3.10
- numpy < 2
- PyQt6
- pyqtgraph
- cv2
- cv2-enumerate-cameras

pyMultiVideo has only been tested on Windows 11. In principle, it could run cross platform, however the installation scripts are written only for Windows.

### Installation 

Administrative access is required to install this application on your machine. This is because the python environment is installed in `C:\Program Files`.

Installation scripts have been developed to install for all users (`C:\Program Files`) only (i.e. installation as an administrator for the computer you intend to install it on). 