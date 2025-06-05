## Will this application drop frames?

This will depend on the implementation of the camera API used.

This current release of the application has support FLIR cameras using the spinnaker-python API. Other video acqusition piplines could drop frames.

pyMultiVideo's interface with the spinnaker camera has functionality to avoid this problem.

This is done in two ways:

#### Internal Buffer Handling

- The camera's internal buffer handling mode is set to overwrite the oldest image first if the buffer is full. This means that if the buffer is starting to fill up, the camera will not overwrite images that have yet to be moved over the camera and into the host machine. (See [here](https://www.teledynevisionsolutions.com/en-gb/support/support-center/application-note/iis/understanding-buffer-handling/) for further information from the manufacturer.)

```python
# Set Buffer handling mode to Oldest First
bh_node = PySpin.CEnumerationPtr(self.stream_nodemap.GetNode("StreamBufferHandlingMode"))
bh_node.SetIntValue(bh_node.GetEntryByName("OldestFirst").GetValue())
```

#### Frequency of buffer emptying

2. Every time the frames are sent to the program to be encoded, all of the images currently in the buffer are retrieved (until no more are left). This ensures that the buffer is continuously being emptied, making sure that the buffer never approaches being full.
   This is implemented as follows.

```python
"""Gets all available images from the buffer and return images GPIO pinstate data and timestamps."""
img_buffer = []
timestamps_buffer = []
gpio_buffer = []
# Get all available images from camera buffer.
try:
    while True:
        next_image = self.cam.GetNextImage(0)  # Raises exception if buffer empty.
        img_buffer.append(next_image.GetNDArray())  # Image pixels as numpy array.
        chunk_data = next_image.GetChunkData()  # Additional image data.
        timestamps_buffer.append(chunk_data.GetTimestamp())  # Image timestamp (ns?)
        frame_number = chunk_data.GetFrameID()
        if (frame_number - self.last_frame_number) != 1:
            print(f"Dropped frame, frame counter diff: {frame_number - self.last_frame_number}")
        self.last_frame_number = frame_number
        if self.camera_model == "Chameleon3":
            img_data = next_image.GetData()
            gpio_buffer.append([(img_data[32] >> 4) & 1, (img_data[32] >> 5) & 1, (img_data[32] >> 7) & 1])
        else:
            gpio_binary = format(chunk_data.GetExposureEndLineStatusAll(), "04b")
            gpio_buffer.append([int(gpio_binary[3]), int(gpio_binary[1]), int(gpio_binary[0])])
        next_image.Release()  # Clears image from buffer.
except PySpin.SpinnakerException:  # Buffer is empty.
    if len(img_buffer) == 0:
        return
    else:
        return {
            "images": img_buffer,
            "gpio_data": gpio_buffer,
            "timestamps": timestamps_buffer,
        }
```

### Will there be support for my camera?

At the moment there is only support for FLIR cameras using the PySpin API that written for python.

If you would like to implement your own camera you can! Click here for more information
