# Camera API

## Adding support for new cameras for pyMultiVideo

Due to this structure of pyMultiVideo it is possible for you to add support for new cameras that haven't been implemented.

At the moment the Spinnaker Cameras are the only ones that have been supported.
Tested on:

- Blackfly
- PointGrey

This should be relatively easy to do by following the instructions in this page as well as looking at the `/camera_api/spinnaker.py` file

Inside the `camera_api/` directory, there is a `generic_camera.py` file that you should take a look at. It contains a template for all the functions that must be implemented for the new camera you are trying to implement to get to work.

Duplicate this file to begin!

<!-- You must rename the file to the name of the module class you are about to implement (e.g. `spinnaker.py` implements the `spinnaker` class). This naming the the way pyMultiVideo knows the name of the class it should inherit from the module.  -->
```python
# Place holder function which returns a list of the available cameras.
#     The should be uniquly idenified as a string.
    
    # naming format requirements: NUMBERS-MODULENAME
    # type(name) == str
```

I have impose a structure for what is a valid camera_api module. there are 3 requirments:

1. The new camera class inherits from the `generic_camera` class
2. There is a `list_available_cameras` function
3. There is a `initialise_by_id` function.

If these functions are not available, the camera_api will not be able to import your new written API. You can include more functions if this is helpful for implementing the core functions set out by the camera class.

## Camera API classes

### Introduction

Located in this folder are two camera classes (each in a different file (e.g. [spinnaker_camera.py](/tools/camera/spinnaker_camera.py)))

In this example you can see different core functions of the camera api that are defined.

These functions are then used in the main GUI of the application to perform the required functionality.

### Add new classes

You may want to add new camera support to the application. To do this, you should add a new python file to the `/camera` directory.

Within this you should define the behaviour required by the functions. For example the  new_camera.get_next_image() should return a np.ndarray from the function as has been done in the spinnaker_camera.get_next_image() function does.

This should be done for all the functions that are defined in the spinnaker camera and the

### Trigger Recording from Camera API

- There is theoretical functionality to trigger recording the GUI by adding functionality to the functions `trigger_start_recording` and the `trigger_end_recording` functions. You might want to use the GPIO pin states to do this.
- These functions are called every time the GUI is refreshed. If these function return `True`, then they will trigger starting and ending recording respectively.
