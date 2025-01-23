# Adding support for new cameras for pyMultiVideo
Due to this structure of pyMultiVideo it is possible for you to add support for new cameras that haven't been implemented. 

At the moment the Spinnaker Cameras are the only ones that have been supported. 
Tested on: 
- Blackfly
- PointGrey

This should be relatively easy to do by following the instructions in this page as well as looking at the `/camera_api/spinnaker.py` file

Inside the `camera_api/` directory, there is a `generic_camera.py` file that you should take a look at. It contains a template for all the functions that must be implemented for the new camera you are trying to implement to get to work. 

Duplicate this file to begin!

<!-- You must rename the file to the name of the module class you are about to implement (e.g. `spinnaker.py` implements the `spinnaker` class). This naming the the way pyMultiVideo knows the name of the class it should inherit from the module.  -->

I have impose a structure for what is a valid camera_api module. there are 3 requirments: 

1. The new camera class inherits from the `generic_camera` class
2. There is a `list_available_cameras` function
3. There is a `initialise_by_id` function.

If these functions are not available, the camera_api will not be able to import your new written API. You can include more functions if this is helpful for implementing the core functions set out by the camera class. 