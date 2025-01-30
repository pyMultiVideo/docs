#

## Using the GUI


![Start-up GUI](/media/start-up-gui.png)
*Example GUI on startup*

### Start recording

To start recording you must enter a `Subject ID`, the click record.

If all the viewfinder widgets have `Subject ID`, then buttons in the `Control All` box will be clickable. This allows you to start and stop recording all the cameras that are being used at once.

### Changing the saving directory of the save data

- The default save directory is `/data` folder. This is where the output from the camera is saved to disk as well as the metadata files
- This can be changed by clicking the "File" icon and selecting the new directory

### Selecting a GPU for encoding

- The applicaiton uses `ffmpeg` to encoder the video to disk. FFMPEG has lots of option for how to encoe the video. To use a GPU you should select 'GPU' on the `FFMPEG Settings` to encode using the graphics processing unit. 

## Other features

### GPIO Pin states Visualisation

If the GPIO states that are being send to the camera are being detected correctly there the `GPIO States:` will become white every time the GPIO pin states get a signal.

### Full Screen Mode

In the Tool bar there is a `View` button which contains a toggle to remove (and re-open) the control buttons which is useful for making viewfinder from the camera as big as possible.

### Opening from Config files

- Get the config file from the `/experiments` folder and use that as the input to the `--config` argument

## Cameras Tab

- Cameras can be renamed. Other various settings for the cameras can be set here.

> Note: If you change the camera settings, you need to re-initialised the camera to see changes in viewfinder's aquisition of data.
