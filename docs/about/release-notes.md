# Release Notes

---

## Maintenance team

* [Alif Aziz](https://github.com/alifuaziz) <alif.aziz@psy.ox.ac.uk>
* [Thomas Akam](https://github.com/ThomasAkam) <thomas.akam@psy.ox.ac.uk>

## Change log

## Version 1.0.0

Key features:

GUI:

* Mutliple video acquisition by instantiating multiple camera API objects at once.
  * GUI to display the video streaming from all cameras being used at once.
  * GUI layout can be saved to *.json* files and loaded. 
  * Video files can be named easily. 

Video Acquisition:

* Use of *ffmpeg* to encode video and save it to disk

* Aquisition settings configurable: Frame rate, Gain, Exposure Time, downsampling
  * Camera settings automatically saved and used after the first start up of the application.
  * Preview of the aquisition of the camera whilst setting acquisition configuration

Spinnaker:

* Implemented reading the GPIO pins from the each image returned from the camera (spinnaker)
* Buffer handling implemented as to not prevent dropped frames.
