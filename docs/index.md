## pyMultiVideo

>**Open source, Python based, Multiple video acquisition.**

![example](./media/multi-screen-layout.jpeg)
*pyMultiVideo displaying and recording video from multiple cameras at once*

*Key Features*

- `pyMultiVideo` is an application for aquiring images from mulitple cameras simulaneously. This is primarily a scientific application.
- This is a `python 3.10` implementation with GUI written using the [QT framework](https://www.qt.io/product/framework) to see the videos you are aquiring real-time.
- Teledyne's Spinnaker API integration is a key feature of this application.

### Recommended Usage

Synchronised video capture from multiple cameras.

### Currently Supported Cameras

PySpin Spinnaker Camera

Tested on:

- `Pointgrey Chameleon3`
- `BlackFlyS`

## Getting started

See [here](./user-guide/installation.md) for instructions on how to install this application.

### Dependencies

pyMultiVideo has the following dependencies

- python 3.10
- numpy < 2
- PyQt6
- pyqtgraph

pyMultiVideo has only been tested on Windows 11. In principle, it could run cross platform.
