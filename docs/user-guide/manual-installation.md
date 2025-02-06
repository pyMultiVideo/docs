# Manual Installation

## Installation

*ffmpeg*

1. Download and install ffmpeg and add it to path
   - A script that is fairly robust is provided for this, otherwise the website to download it here `https://www.ffmpeg.org/download.html`
  
*miniconda*

1. Download and install miniconda
      - Follow the Webstite instructions here
      - `https://docs.anaconda.com/miniconda/`

2. Create a conda environment in which to install the application 
      - If this is the first time you are installing this application, you might need to run `conda init` and then restart the powershell instance.
      - Run `conda create -n pmv python=3.10` to create a python environment with python 3.10 installed
      - Activate this environment: `conda activate pmv`
3. Install the required python packaged into this conda environment (distributed by pip)
       - Locate the `requirements.txt` in the `path/to/code/requirements.txt`
       - Install the python packages in the `requirements.txt` using the command: `pip install -r /path/to/code/requirements.txt`

*Spinnaker SDK*


1. Download and install the Spinnaker SDK and PySpin API
      - Log into the website `https://www.teledynevisionsolutions.com/support/support-center/software-firmware-downloads/iis/spinnaker-sdk-download/spinnaker-sdk--download-files/?pn=Spinnaker+SDK&vn=Spinnaker+SDK`
      - Download the latest Spinnaker SDK available e.g. 'Spinnaker FUll SDK 4.0.0.116'
      - Download the latest Python SDK available e.g. 'Windows Python Spinnaker SDK 4.0.0.116'
2. Extract the .zip file and install full windows installer.
      - This will install the drivers for the cameras
3. Extract the .zip file for the Python Spinnaker SDK to a known location. 
4. Install the PySpin (not distributed by pip)
       - In the spinnaker SDK, you will see file called `.whl`
       - Copy the path to the `.whl` file 
       - Install it in the miniconda environment created above: e.g. `pip install "path/to/sdk/spinnaker_python-4.0.0.116-cp310-cp310-win_amd64.whl"`
## Lanch Application 

- Activate the conda environment e.g. `conda activate pmv`
- Launch the python application from the active python environment: `python path/to/pyMultiVideo_GUI.pyw`