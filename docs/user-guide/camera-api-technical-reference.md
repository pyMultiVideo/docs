# Camera API Techinical Reference

### GenericCamera

#### `__init__`

```python
```

#### get_height()

```python
GenericCamera.get_height()
```

Get the height of the image acquired from the GenericCamera

#### get_width()

```python
GenericCamera.get_width()
```

Get the width of the image acquired from the GenericCamera

#### get_frame_rate_range(*exposure_time)

```python
```

Get the range of frame rates that are available to the GenericCamera for a given `exposure_time`.

`exposure_time` is an option argument that is used in case the GenericCamera.get_frame_rate_range() needs to calculate it directly.

returns a tuple of `int`s

#### get_frame_rate()

```python
GenericCamera.get_frame_rate()
```

Returns a `float` of the camera's frame rate.

#### get_gain()

```python
GenericCamera.get_gain()
```

Returns a `float` of the camera's gain.

#### get_gain_range()

```python
GenericCamera.get_gain_range()
```

Get the range of gain values that are available to the GenericCamera.

Returns the gain range as a tuple of `int`s

#### get_exposure_time_range(*fps)

```python
GenericCamera.get_exposure_time_range(fps)
```
Get the range of frame rates that are available to the GenericCamera for a given `fps`.

`fps` is an option argument that is used in case the GenericCamera.get_frame_rate_range() needs to calculate it directly.

Returns a tuple of fps range as a tuple of `int`s

#### get_exposure_time()

```python
GenericCamera.get_exposure_time()
```

Get the current exposure time of the GenericCamera in microseconds

returns a `float`

#### set_acqusition_mode(external_trigger)

```python
GenericCamera.set_acqusition_mode(external_trigger)
```

#### set_frame_rate(frame_rate)

```python
GenericCamera.set_frame_rate(frame_rate)
```

Set the frame rate of GenericCamera to `frame_rate`

#### set_exposure_time(exposure_time)

```python
GenericCamera.set_exposure_time(exposure_time)
```

Set the exposure time of GenericCamera to `exposure_time`

#### set_gain(gain)

```python
GenericCamera.set_gain(gain)
```

Set the gain of GenericCamera to `gain`

#### set_pixel_format(pixel_format)

```python
```

Set the frame rate of GenericCamera to `frame_rate`

#### begin_capturing(CameraConfig)

```python
```

#### stop_capturing

```python
```

#### close_api

```python
```

#### get_available_images

```python
```

### list_available_cameras

```python
list_available_cameras(VERBOSE=False)
```

returns a `list` of the `unique_id`s that will be used to initialise the cameras.

These unique_id s must be different to eachother otherwise the application will have undefined behaviour when the `unique_id` are the same for two different cameras.

All `unique_id` must be in the format   `<module>-<camera_module_name>`. For example the spinnaker unique_id  will all be the format `<serial_number>-spinnaker` since the camera_api for the Spinnaker cameras is called `spinnaker.py`

`VERBOSE` will tell the function to print out the names of the `unique_id`s that are generated. Useful for debugging.

### initialise_camera_api

```python
initialise_camera_api(CameraConfig)
```

returns instance of the `GenericCamera` class with the settings `CameraConfig`. If none is parsed, default settings are using for initialsation.
