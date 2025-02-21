
## Can't open the GUI

To open the GUI you must run the   `pyMultiVideo_GUI.pyw`. Furthermore the python files must be opened using the python virtual environment that has been setup using the installation scripts. This means activating the conda environment created using `miniconda`, then using this verison of python to run the `pyMultiVideo_GUI.pyw`.

To do this manually:

1. Run `conda env list` to show the list of conda environments
2. You should see a list of the conda python enviroments, including one called `C:\Program Files\miniconda3\envs\pyMultiCam_env`
3. Run `conda activate C:\Program Files\miniconda3\envs\pyMultiCam_env` to activate this conda environment.
4. Run `python path/to/code/pyMultiVideo_GUI.pyw` to open the python application.

### I want to double click `pyMutliVideo_GUI.pyw` and open the GUI without using terminal

In the `code/` directory, there is a file called `LAUNCH_GUI.bat` that contains a script that can be doubled clicked and will launch a terminal application in which pyMultiVideo will launch. 

## `conda` hasnt been added to path

![Not added to path](/media/conda-not-added-to-path.png)

For the powershell script to work, it must know the conda command. The powershell requires that you add the installation location of miniconda to the environment variables for the machine.

Do this by adding the following directories to PATH: `C:\Program Files\miniconda3;C:\Program Files\miniconda3\Scripts;C:\Program Files\miniconda3\Library\bin`

[This](https://stackoverflow.com/questions/44597662/conda-command-is-not-recognized-on-windows-10) is a link to a stack exchange post which might be helpful.

If you have downloaded and installed miniconda using the scripts provided in the `_installation/` directory then this is where miniconda has been installed.

You can check that this has been successful by navigating to the `C:\Program Files` folder. Here you should see a file called `miniconda` This means miniconda has been installed correctly.

## FileNotFoundError: FFmpeg binary not found. Please install FFmpeg and ensure it's in your PATH

This error has occured because `ffmpeg` has not been added to your PATH (or your evironment variables). This should've been done by the ffmpeg installation script. Make sure you have done this. You can confirm this by typing `ffmpeg -version` and seeing the following as your terminal output:

```powershell
ffmpeg version 7.1-essentials_build-www.gyan.dev Copyright (c) 2000-2024 the FFmpeg developers
built with gcc 14.2.0 (Rev1, Built by MSYS2 project)
configuration: --enable-gpl --enable-version3 --enable-static --disable-w32threads --disable-autodetect --enable-fontconfig --enable-iconv --enable-gnutls --enable-libxml2 --enable-gmp --enable-bzlib --enable-lzma --enable-zlib --enable-libsrt --enable-libssh --enable-libzmq --enable-avisynth --enable-sdl2 --enable-libwebp --enable-libx264 --enable-libx265 --enable-libxvid --enable-libaom --enable-libopenjpeg --enable-libvpx --enable-mediafoundation --enable-libass --enable-libfreetype --enable-libfribidi --enable-libharfbuzz --enable-libvidstab --enable-libvmaf --enable-libzimg --enable-amf --enable-cuda-llvm --enable-cuvid --enable-dxva2 --enable-d3d11va --enable-d3d12va --enable-ffnvcodec --enable-libvpl --enable-nvdec --enable-nvenc --enable-vaapi --enable-libgme --enable-libopenmpt --enable-libopencore-amrwb --enable-libmp3lame --enable-libtheora --enable-libvo-amrwbenc --enable-libgsm --enable-libopencore-amrnb --enable-libopus --enable-libspeex --enable-libvorbis --enable-librubberband
libavutil      59. 39.100 / 59. 39.100
libavcodec     61. 19.100 / 61. 19.100
libavformat    61.  7.100 / 61.  7.100
libavdevice    61.  3.100 / 61.  3.100
libavfilter    10.  4.100 / 10.  4.100
libswscale      8.  3.100 /  8.  3.100
libswresample   5.  3.100 /  5.  3.100
libpostproc    58.  3.100 / 58.  3.100
```

## Conda not initialised

- When installing the software you may see a error that asks you to `Run 'conda init' before 'conda activate'` This usually happens on first installation of miniconda.
- It requires you to run `conda init`, then restart the powershell instance. You can check if `conda activate` works by running this command before running the installation script again. There shuld be no red error message if `conda activate` has run correctly.

![Not initalised](/media/conda-not-initialised.png)

## Spinnaker Cameras have not shown up in the GUI

This likely due to the Spinnaker drivers not being installed correctly.

In this case, you should check that the drivers are working in `Spinview`, spinnaker's own recording application, which has more explicit error message for drivers.

If you see something like the following image, then you might have a problem with your drivers. I am not 100% sure why this occurs, however reinstalling the spinnaker drivers from their website might be able to fix it.
![bad drivers](/media/driver-problem.png)

Note: that you camera should likely appear like the following image the device manager, and not as a USB camera for correct installation:

![device-managed-view](/media/flir-camera-drivers-view.png)

## Flickering of the viewfinder

The update rate of the GUI is different to the update rate. This could also be fixed by updating the drivers for the camera.

## Firewall screen

When you are first running the applicaiton a firewall could warning for running the python executable.

![fire-wall-screen](/media/python-firewall.png)