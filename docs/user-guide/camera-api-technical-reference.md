# Camera API Techinical Reference

## Introduction

The current APIs that are supported are:

- PySpin Spinnaker API

In development:

- Ximea Python API
- OpenCV API (for Webcams)

If you would like to support your own brand of cameras, you will need to write your own API for pyMultiVideo. This requires createing a python module (e.g. `new.py`). This `NewCamera` class will handle the required functionality of the that is required to be defined for pyMutliVideo.

## GenericCamera

### `__init__`

Function that runs in instantiation of the GenericCamera.

There are attributes of the camera that are access by pyMutliVideo that must be defined:

```python
self.serial_number = None  # To be replaced with device serial number.
self.device_model = "GenericCameraModel"  # Replace with the camera model name to be recorded in metadata.
self.N_GPIO = 3  # Number of pins that the camera records each frame.
self.trigger_line = None  # Name of the line which will be used to trigger external acqusition
self.manual_control_enabled = (
    False  # If true, there is manual control available for the camera (gain / exposure time)
)
```

The GenericCamera might also have code runs to ensure that the camera has been started with the correct settings (e.g. setting the buffer size, configuring information about what metadata comes from each image or acqusing images in manual mode without image processing happening on device)

### get_height()

```python
GenericCamera.get_height()
```

Get the height of the image acquired from the GenericCamera

### get_width()

```python
GenericCamera.get_width()
```

Get the width of the image acquired from the GenericCamera

### get_frame_rate_range(\*exposure_time)

```python
GenericCamera.get_frame_rate_range(*exposure_time)
```

Get the range of frame rates that are available to the GenericCamera for a given `exposure_time`.

`exposure_time` is an option argument that is used in case the GenericCamera.get_frame_rate_range() needs to calculate it directly.

returns a tuple of `int`s

### get_frame_rate()

```python
GenericCamera.get_frame_rate()
```

Returns a `float` of the camera's frame rate.

### get_gain()

```python
GenericCamera.get_gain()
```

Returns a `float` of the camera's gain.

### get_gain_range()

```python
GenericCamera.get_gain_range()
```

Get the range of gain values that are available to the GenericCamera.

Returns the gain range as a tuple of `int`s

### get_exposure_time_range(\*fps)

```python
GenericCamera.get_exposure_time_range(fps)
```

Get the range of frame rates that are available to the GenericCamera for a given `fps`.

`fps` is an option argument that is used in case the GenericCamera.get_frame_rate_range() needs to calculate it directly.

Returns a tuple of fps range as a tuple of `int`s

### get_exposure_time()

```python
GenericCamera.get_exposure_time()
```

Get the current exposure time of the GenericCamera in microseconds

returns a `float`

### set_acqusition_mode(external_trigger)

```python
GenericCamera.set_acqusition_mode(external_trigger)
```

### set_frame_rate(frame_rate)

```python
GenericCamera.set_frame_rate(frame_rate)
```

Set the frame rate of GenericCamera to `frame_rate`

### set_exposure_time(exposure_time)

```python
GenericCamera.set_exposure_time(exposure_time)
```

Set the exposure time of GenericCamera to `exposure_time`

### set_gain(gain)

```python
GenericCamera.set_gain(gain)
```

Set the gain of GenericCamera to `gain`

### set_pixel_format(pixel_format)

```python
GenericCamera.set_pixel_format(pixel_format)
```

Set the pixel format to pixel format

### begin_capturing(CameraConfig)

```python
GenericCamera.begin_capturing(CameraConfig)
```

Begins the camera capturing images with the `CameraConfig`. If none is passed, the camera will begin capturing with the current settings of the camera.

### stop_capturing

```python
GenericCamera.stop_capturing()
```

Ends the capturing of video from the GenericCamera

### close_api

```python
GenericCamera.close_api()
```

Shuts down the GenericCamera and releases any memory allocation that is might be using (such as buffer allocation), if this important for the camera's functionality.

### get_available_images

```python
GenericCamera.get_available_images()
```

Returns a `dict` of the images that have accumulated in the buffer since the last time the function was called.

The `dict` takes the following form:

```python
Returns:
    {
    "images" : img_buffer - a list of images (as byte arrays)
    "gpio_data" : gpio_buffer - a corresponding list of gpio data for each of the frames
    "timestamps" : timestamps_buffer - a corresponding list of timestampes for each frame
    "dropped_frames": dropped_frames - a int of the number of frames that have been dropped
    }:
```

It is important that this functionality is implemented correctly as the GUI displaying the relevent information will only be able to display this, if parsed correctly to it.

The rate of this function call is defined in `code/config/config.py` under the `gui_config["camera_update_rate"]` in Hz.

Recommended pseudocode format for implementing this function:

```python
# Instantiate new temp buffers
img_buffer = []
GPIO_buffer = []
timestamps_buffer = []
dropped_frames = 0
try:
  while True:
        image = cam.get_next_image(timeout=0) # The `get_next_image` function waits for an image until timeout seconds elapse, then raises an error. Setting timeout=0 empties all images from the buffer immediately, raising an error once none are left. This is the recommended way to flush the camera's internal buffer.
        img_buffer.append(image.get_byte_data()) # Get the data in bytes
        GPIO_buffer.append(image.get_GPIO_data()) # Get the pin states from the image
        timestamps_buffer.append(image.get_timestamp()) # Get the timestampe from the image
        if dropped_frames: # Check for dropped frames
            dropped_frames += 1
except EmptyBufferError:
 # Only returns images if there are images to be returned
    if len(img_buffer) == 0:
        return
    else:
        return
        {
            "images" : img_buffer
            "gpio_data" : GPIO_buffer
            "timestamps" : timestamps_buffer
            "dropped_frames": dropped_frames
        }
```

## list_available_cameras

```python
list_available_cameras(VERBOSE=False)
```

returns a `list` of the `unique_id`s that will be used to initialise the cameras.

These unique_id s must be different to eachother otherwise the application will have undefined behaviour when the `unique_id` are the same for two different cameras.

All `unique_id` must be in the format `<module>-<camera_module_name>`. For example the spinnaker unique_id will all be the format `<serial_number>-spinnaker` since the camera_api for the Spinnaker cameras is called `spinnaker.py`

`VERBOSE` will tell the function to print out the names of the `unique_id`s that are generated. Useful for debugging.

## initialise_camera_api

```python
initialise_camera_api(CameraConfig)
```

returns instance of the `GenericCamera` class with the settings `CameraConfig`. If none is parsed, default settings are using for initialsation.
