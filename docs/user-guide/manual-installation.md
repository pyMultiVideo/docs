
# Installation

The installation of this application requires downloading the python source code from pyMultiVideo/code and setting up the python virtual environment in which to run the application.

## Downloading the source code

- If you are using the *git bash* terminal, simply navigate to the folder you would like to code to be stored in (`cd path/to/code`)
- Clone the repositiory to the desired location: `git clone https://github.com/pyMultiVideo/code.git`

For further information on cloning github repositiory please see [here](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) for official documentation.

## Creating the python environment

The installation of the application has 3 main steps:

- Installing FFMPEG
- Setting up the python environment
- Installing the Spinnaker python API into the python environment.

### 1. FFMPEG

1. Download and install FFPEG and add it to path
   - A script that is fairly robust is provided for [here](https://gist.github.com/AnjanaMadu/5f9689e9572492a50089f4a74b9b8de5), otherwise the website to download it here `https://www.ffmpeg.org/download.html`
   - If you have troube opening this file, you can copy and paste the contents of this file into powershell directly to run it

### 2. Miniconda

1. Download and install miniconda
      - Follow the Webstite instructions here (direct download link [here](https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe))
      - `https://docs.anaconda.com/miniconda/`

2. Create a conda environment in which to install the application
      - If this is the first time you are installing this application, you might need to run `conda init` and then restart the powershell instance.
      - Run `conda create -n pmv python=3.10` to create a python environment with python 3.10 installed
      - Activate this environment: `conda activate pmv`
3. Install the required python packaged into this conda environment (distributed by pip) using the requirements.txt
      - Clone the `pyMultiVideo/code` to a known location.
      - Locate the `requirements.txt` in the `path/to/pyMutliVideo/code/` repository
      - Install the python packages in the `requirements.txt` using the command: `pip install -r /path/to/pyMultiVideo/code/requirements.txt`

### 3. Spinnaker SDK

1. Download and install the Spinnaker SDK and PySpin API
      - Log into the website `https://www.teledynevisionsolutions.com/support/support-center/software-firmware-downloads/iis/spinnaker-sdk-download/spinnaker-sdk--download-files/?pn=Spinnaker+SDK&vn=Spinnaker+SDK`
      - Download the latest Spinnaker SDK available e.g. [Spinnaker FUll SDK 4.0.0.116](https://flir.netx.net/file/asset/59416/original/attachment)
      - Download the latest Python SDK available e.g. [Windows Python Spinnaker SDK 4.0.0.116](https://flir.netx.net/file/asset/59416/original/attachment)
2. Extract the .zip file and install full windows installer.
      - This will install the drivers for the cameras
3. Extract the .zip file for the Python Spinnaker SDK to a known location.
4. Install the PySpin (not distributed by pip)
       - In the spinnaker SDK, you will see file with the extention `.whl`
       - Copy the path to the `.whl` file
       - Ensure that the conda environment `pmv` has been activated using the `conda activate pmv` command.
       - Install it in the miniconda environment created above: e.g. `pip install "path/to/sdk/spinnaker_python-4.0.0.116-cp310-cp310-win_amd64.whl"`

The installation in complete!

## Lanch Application

- Activate the conda environment e.g. `conda activate pmv`
- Launch the python application from the active python environment: `python path/to/pyMultiVideo_GUI.pyw`
- To launch from the file explorer double click the `LAUNCH_GUI.bat` which runs the commands described above. A shortcut to this file can be made to launch this application from elsewhere.
