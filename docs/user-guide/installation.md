# Installation

## Dependencies

pyMultivideo requires a Python 3 installation with the following packages:

- numpy
- PyQt6
- pyqtgraph
- opencv-python
- pyserial

Additional Python modules are required for interacting with different camera systems, only modules for camera systems you will use need to be installed.

- PySpin - for controlling FLIR cameras through the [Spinnaker SDK](https://www.teledynevisionsolutions.com/products/spinnaker-sdk/).
- ximea - for controlling Ximea cameras.

We recommend creating a dedicated Miniconda environment for pyMultivideo as detailed in the instructions below.  PySpin is only compatible with Python 3.10 so this Python version was used for all testing.

pyMultivideo uses [ffmpeg](https://www.ffmpeg.org/) to compress and save videos, so requires it to be installed and on the system path such that ffmpeg can be run from the command line with the `ffmpeg` command.

To compress videos on the GPU it is necessary to have an NVIDIA GPU that supports NVENC video encoding.  Most modern NVIDA GPUs have this functionality but you can check specific models [here](https://developer.nvidia.com/video-encode-and-decode-gpu-support-matrix-new).  If you need to buy a GPU specifically for this application, the RTX A400 is a good option as it is cheap, compact and is powered only via the PCI slot, so can be installed in most standard office desktops.  If you have a compatible GPU then it is recommended to install the latest Studio Driver for your graphics card from the [driver downloads](https://www.nvidia.com/en-us/drivers/) page.

We have only tested pyMultiVideo on Windows 10 and 11.

## Step-by-step installation guide

### Get the pyMultiVideo code

The recommended way to get pyMultiVideo is to clone the repository <https://github.com/pyMultiVideo/code> as this makes it straightforward to update the application when new versions are released by pulling the latest version from the repository.  

- If you are using the [_git bash_ terminal](https://gitforwindows.org), simply navigate to the folder you would like to code to be stored in (`cd path/to/code`)
- Clone the repository to the desired location: `git clone https://github.com/pyMultiVideo/code.git`
- Alternatively you clone the repository using a git client with a graphical interface such as [Github Desktop](https://github.com/apps/desktop).

For further information on cloning github repositories see the [Github documentation](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository).

### Install ffmpeg

1. Download the latest Windows ffmpeg release as a zip file from this link <https://www.gyan.dev/ffmpeg/builds/ffmpeg-release-essentials.zip>.
2. Extract the zip file. The unzipped folder will contain a folder named something like `ffmpeg-7.1-essentials_build`, rename this `ffmpeg` and copy it to `C:\Program Files`.
3. Add the folder `C:\Program Files\ffmpeg\bin` which contains the `ffmpeg.exe` executable to the system path, so that ffmpeg can be launched from the command line. To do this:

   1. In the windows search bar enter `environment variables` and select `Edit the System Environment Variables` to open the `System Properties` dialog.
   2. Click the `Environment Variables` button to open the `Environment Variables` dialog.
   3. In the `System variables` box select the `Path` item and click `Edit` to open the `Edit environment variable` dialog.
   4. Click `New` and then paste in the path to the ffmpeg bin folder, e.g. `C:\Program Files\ffmpeg\bin`. Close the dialog boxes by clicking OK.

4. Check ffmpeg can be run from the command line by opening a windows command prompt and entering `ffmpeg`. If ffmpeg is installed successfully you will see information about the ffmpeg configuration. If not you will get a message saying _'ffmpeg' is not recognised_.

### Install miniconda and create environment

1. Download the latest windows Miniconda installer from the link: <https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe>.
2. Run the installer and follow the instructions to install Miniconda for all users. Make sure you note where miniconda is installed.
3. Add the miniconda `Scripts` directory (typically `C:\ProgramData\miniconda3\Scripts` for a default install) to the system path as detailed above so that you can run the `conda` command from the windows command line.
4. Open a window command prompt and enter `conda init` then close and reopen the command prompt.
5. Run `conda create -n pmv python=3.10` to create a conda environment called `pmv` using Python 3.10.
6. Activate the environment with the command `conda activate pmv`
7. Install the required python packaged into the conda environment:

   1. Change directory to the pyMultiVideo code folder that contains the file `requirements.txt` using `cd path/to/code/folder`.
   2. Install the python packages with `pip install -r requirements.txt`

### Install required camera system modules:

Install Python modules for interfacing with camera systems, currently the FLIR Spinnaker and Ximea Python APIs  are supported by pyMultivideo.  You only need to install Python modules for camera systems you are going to use.

#### Install the Spinnaker SDK and PySpin python package

1. Go to the [Spinnaker SDK Download](https://www.teledynevisionsolutions.com/support/support-center/software-firmware-downloads/iis/spinnaker-sdk-download/spinnaker-sdk--download-files/?pn=Spinnaker+SDK&vn=Spinnaker+SDK) page. You will need to create an account on the Teledyne website to access the downloads.
2. Download the latest version of the main Spinnaker SDK for windows (e.g. `SpinnakerSDK_FULL_x.x.x.x_x64.exe`) and the Python 3.10 bindings (e.g. `spinnaker_python-x.x.x.x-cp310-cp310-win_amd64.zip`)
3. Run the Spinnaker SDK installer and select the `Application Development` installation profile.
4. Unzip the .zip file containing the spinnaker python bindings. This contains a .whl file (e.g. `spinnaker_python-x.x.x.x-cp310-cp310-win_amd64.whl` used to install the PySpin module using pip:

   1. Open a windows command promp and `cd` to the folder containing the .whl file.
   2. Activate the `pmv` conda environment with the command `conda activate pmv`.
   3. Install the PySpin module from the .whl file with the command: `pip install spinnaker_python-4.2.0.83-cp310-cp310-win_amd64.whl`.

##### Installation of BlackFly camera

The standard [BlackFlyS](https://www.teledynevisionsolutions.com/en-gb/products/blackfly-s-usb3/?vertical=machine+vision&segment=iis) camera firmware does not implement PySpin access to all the camera frame metadata needed by pyMultivideo.   The manufacturers of the BlackFlyS cameras (Teledyne/FLIR) do not have a timeline for fixing this issue in the production firmware, but provided a download link for a beta version of the firmware in which it has been fixed.  The steps for the firmware upgrade are as follows:

1. Complete the normal installation of pyMultiVideo.
2. Download the beta firmware for the BlackFlyS camera to a known location from this link:
   [https://teledyne.app.box.com/s/j4tkdvyi7xlym1baxv5g0cm8mlygcwdv](https://teledyne.app.box.com/s/j4tkdvyi7xlym1baxv5g0cm8mlygcwdv)
3. Download and open [Spinview](https://softwareservices.flir.com/Spinnaker/latest/_spin_view_guide.html) application.
4. Upgrade the BlackFlyS camera firmware by following the following steps (see also [this](https://support.swingcatalyst.com/hc/en-us/articles/360018779740-Upgrading-the-firmware-on-the-FLIR-Blackfly-S) guide).
   - Find the camera in the 'Devices' menu.
   - Right click the camera and select 'Update Device Firmware'
   - A pop-up will show up where you should select the `.ez2` firmware file downloaded in Step 2.
   - Click 'Start' and OK the warning to not disconnect the camera during the firmware update.

#### Install the Ximea python API

1. Go to the [Ximea Windows Software Package](https://www.ximea.com/support/wiki/apis/XIMEA_Windows_Software_Package) page and download the Long Term Support (LTS) version of the tool. You will need to create an account on the Ximea wedsite to access the downloads.
2. Run the executable file downloaded (`XIMEA_Windows_SP_Stable.exe`)
3. Nagivate to the location of the installation folder (e.g. `C:\XIMEA`), then locate the API (`C:\XIMEA\API\Python\v3\ximea`) This is the folder that contains the python library you will install.

4. Locate the site-packages folder for the miniconda environment by doing the following:

   1. Activate the conda environment `conda activate pmv`,
   2. Run `conda info`, then locate the `active env location`. This will look like `C:\miniconda3\envs\pmv` if this is installed for all users
   3. Locate the `\Lib\site-packages` folder. This folder contains the packages you have installed in the pmv environment. The full path should look something like the following `C:\miniconda3\envs\pmv\Lib\site-packages`

5. Copy the `ximea` folder into this folder this installs the ximea python API.

To confirm a successful installation you can import this library into the python environment by opening an instance of `pmv` python environment, then importing ximea (using `import ximea`), then running `ximea.__version__` to check if a version number is returned.

## Launch Application

Double clicking the file `LAUNCH_pyMV.bat` in the pyMultiVideo code folder will activate the conda environment and launch the GUI.

!!! tip "Creating a shortcut"
	To launch the GUI from another folder (e.g, the Desktop), create a shortcut for the LAUNCH_GUI.bat there, and it will still be functional.

Alternatively you can manually activate the conda environment and launch the GUI:

1. Open a windows command prompt and activate the conda environment with `conda activate pmv`.
2. `cd` to the pyMultiVideo code folder that contains the file `pyMultiVideo_GUI.pyw`.
3. Run the GUI with the command `python pyMultiVideo_GUI.pyw`

## Updating pyMultiVideo

If you have obtained the pyMultivideo code by cloning the repository from Github, you can update the software by pulling the latest version from Github.

If you are using git bash:

1. Open git bash (as Administrator if permision are required to do so)
2. Navigate to the pyMultiVideo folder (`cd C:\pyMultiVideo\code`). You should be able to see the name of the branch in brackets `(main)` if this has been done successfully.
3. Run [`git pull`](https://git-scm.com/docs/git-pull) to download any updates that have occured since installing the application

> Note: If you have made any changes to the source code of the application, you will be asked to either [stash](https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning) or discard these changes from the original repo before pulling any further changes.

Alternatively you can use a graphical git client (e.g. Github Desktop) rather than git bash to pull the latest version from Github.

There is no need to re-install the application's _python_ environment or FFMPEG since this should already be installed correctly.

You can check the version number in the window title (e.g. _pyMultiVideo v1.0.0_)
