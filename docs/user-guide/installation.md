# Installation

## Dependencies

pyMultivideo requires a Python 3 installation with the following packages:

- numpy
- PyQt6
- pyqtgraph
- opencv-python
- PySpin

PySpin, the Python bindings for the [Spinnaker SDK](https://www.teledynevisionsolutions.com/products/spinnaker-sdk/) used for controlling FLIR cameras, is only compatible with Python 3.10. We therefore recommend creating a dedicated miniconda environment for pyMultivideo as detailed in the instructions below.

pyMultivideo uses [ffmpeg](https://www.ffmpeg.org/) to compress and save videos, so requires ffmpeg to be installed and on the system path such that ffmpeg can be run from the command line with the `ffmpeg` command.

To compress videos on the GPU it is necessary to have an NVIDIA GPU that supports NVENC video encoding, for information about which GPUs support this see [here](https://developer.nvidia.com/video-encode-and-decode-gpu-support-matrix-new). If you have a compatible GPU then it is recommended to install the latest Studio Driver for your graphics card from the [driver downloads](https://www.nvidia.com/en-us/drivers/) page.

## Step-by-step installation guide

We have only installed and tested pyMultiVideo on Windows 10 and 11.

### Get the pyMultiVideo code

The recommended way to get pyMultiVideo is to clone the repository <https://github.com/pyMultiVideo/code> as this makes it straightforward to update the application when new versions are released by pulling the latest version from the repository.

- If you are using the [_git bash_ terminal](https://gitforwindows.org), simply navigate to the folder you would like to code to be stored in (`cd path/to/code`)
- Clone the repository to the desired location: `git clone https://github.com/pyMultiVideo/code.git`

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

### Install a camera API of your choice:

Currently the Spinnaker SDK and the Ximea API are supported by pyMultivideo:

#### Install the Spinnaker SDK and PySpin python package

1. Go to the [Spinnaker SDK Download](https://www.teledynevisionsolutions.com/support/support-center/software-firmware-downloads/iis/spinnaker-sdk-download/spinnaker-sdk--download-files/?pn=Spinnaker+SDK&vn=Spinnaker+SDK) page. You will need to create an account on the Teledyne website to access the downloads.
2. Download the latest version of the main Spinnaker SDK for windows (e.g. `SpinnakerSDK_FULL_4.2.0.83_x64.exe`) and the Python 3.10 bindings (e.g. `spinnaker_python-4.2.0.83-cp310-cp310-win_amd64.zip`)
3. Run the Spinnaker SDK installer and select the `Application Development` installation profile.
4. Unzip the .zip file containing the spinnaker python bindings. This contains a .whl file (e.g. `spinnaker_python-4.2.0.83-cp310-cp310-win_amd64.whl` used to install the PySpin module using pip:

   1. Open a windows command promp and `cd` to the folder containing the .whl file.
   2. Activate the `pmv` conda environment with the command `conda activate pmv`.
   3. Install the PySpin module from the .whl file with the command: `pip install spinnaker_python-4.2.0.83-cp310-cp310-win_amd64.whl`.

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

Double clicking the file `LAUNCH_GUI.bat` in the pyMultiVideo code folder will activate the conda environment and launch the GUI.

!!! tip "Creating a shortcut"
To launch the GUI from another folder (e.g, the Desktop), create a shortcut for the LAUNCH_GUI.bat there, and it will still be functional.

Alternatively you can manually activate the conda environment and launch the GUI:

1. Open a windows command prompt and activate the conda environment with `conda activate pmv`.
2. `cd` to the pyMultiVideo code folder that contains the file `pyMultiVideo_GUI.pyw`.
3. Run the GUI with the command `python pyMultiVideo_GUI.pyw`
