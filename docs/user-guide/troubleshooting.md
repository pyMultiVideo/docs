## Firewall screen 

When you are first running the applicaiton a firewall could warning for running the python executable.

## Can't open the GUI

To open the GUI you must run the   `pyMultiVideo_GUI.pyw`. Furthermore the python files must be opened using the python virtual environment that has been setup using the installation scripts. This means activating the conda environment created using `miniconda`, then using this verison of python to run the `pyMultiVideo_GUI.pyw`.


To do this manually: 
1. Run `conda env list` to show the list of conda environments 
2. You should see a list of the conda python enviroments, including one called `C:\Program Files\miniconda3\envs\pyMultiCam_env`
3. Run `conda activate C:\Program Files\miniconda3\envs\pyMultiCam_env` to activate this conda environment. 
4. Run `python path/to/code/pyMultiVideo_GUI.pyw` to open the python application. 


## `conda` hasnt been added to path

For the powershell script to work, it must know the conda command. The powershell requires that you add the installation location of miniconda to the environment variables for the machine.

Do this by adding the following directories to PATH: `C:\Program Files\miniconda3;C:\Program Files\miniconda3\Scripts;C:\Program Files\miniconda3\Library\bin`

If you have downloaded and installed miniconda using the scripts provided in the `_installation/` directory then this is where miniconda has been installed. 

You can check that this has been successful by navigating to the `C:\Program Files` folder. Here you should see a file called `miniconda` This means miniconda has been installed correctly.

## Spinnaker Cameras have not shown up in the GUI 

## Flickering of the viewfinder


## Cameras are not changing their settings, despite them being changed in the "Setups Tab"

This might be because of 