#

Other applications have a problem where the spinnaker cameras can drop frames due to the framer buffer full before they are taken from the camera and saved to disk. 

pyMultiVideo's interface with the spinnaker camera has functionality to avoid this problem. 

This is done in two ways: 

1. The camera's internal buffer handleing mode is set to overwrite the oldest image first if the buffer is full. This means that if the buffer is starting to fill up, the camera will not overwrite images that have yet to be moved over the camera and into the host machine. (See [here](https://www.teledynevisionsolutions.com/en-gb/support/support-center/application-note/iis/understanding-buffer-handling/) for further information from the manufacture.)

```
def set_buffer_handling_mode(self, mode: str = "OldestFirst") -> None:
        """
        Sets the buffer handling mode.

        By default, the buffer handling mode is set to 'OldestFirst'. This means that the oldest image in the buffer is the first to be retrieved.

        Alternative modes are:
        - NewestFirst
        - NewestOnly
        - OldestFirstOverwrite

        See: https://www.teledynevisionsolutions.com/en-gb/support/support-center/application-note/iis/accessing-the-on-camera-frame-buffer/

        For this implementation, use of oldest first is important as the camera releases the images in the order they are collected.
        If the buffer is not emptied in this order then the images will be encoded in the wrong order which is bad

        """
        if mode not in ["OldestFirst"]:
            # Raise a warning if the mode is not set to 'OldestFirst'
            self.logger.warning(f"Buffer handling mode '{mode}' is not 'OldestFirst'.")

        try:
            # Access the Transport Layer Stream (TLStream) node map
            stream_nodemap = self.cam.GetTLStreamNodeMap()

            # Set buffer handling mode
            node_buffer_handling_mode = PySpin.CEnumerationPtr(
                stream_nodemap.GetNode("StreamBufferHandlingMode")
            )

            # Check if the node exists and is writable
            if PySpin.IsAvailable(node_buffer_handling_mode) and PySpin.IsWritable(
                node_buffer_handling_mode
            ):
                node_mode_value = node_buffer_handling_mode.GetEntryByName(
                    mode
                )  # Change to desired mode
                if PySpin.IsAvailable(node_mode_value) and PySpin.IsReadable(
                    node_mode_value
                ):
                    node_buffer_handling_mode.SetIntValue(node_mode_value.GetValue())
                    print(
                        f"Buffer Handling Mode set to: {node_mode_value.GetSymbolic()}"
                    )

        except PySpin.SpinnakerException as ex:
            print(f"Error setting buffer handling mode: {ex}")


```

2. Every time the frames are set to the program to be encoded, all of the images currently in the buffer retrieved (until no more are left). This ensures that the buffer is continuously being emptied, making sure that the buffer never approaches being full. 
This is implemented as follows. 
```
self.img_buffer = []
self.gpio_buffer = []
self.timestamps_buffer = []
try:
    while True:
        # Get the next image
        next_image = self.cam.GetNextImage(0)
        # Get information about the image

        next_image.Release()
        self.img_buffer.append(next_image.GetNDArray())
        # Get the GPIO data
        self.gpio_buffer.append(list(self.get_GPIO_data().values()))
        # Get chunk data
        self.timestamps_buffer.append(
            self.get_image_time_stamp(next_image=next_image)
        )

except PySpin.SpinnakerException as e:
    # When the buffer is empty, the 'GetNextImage' function will raise an exception.
    # This marks the end of the buffer.
    # print(f'PySpin Exeception Raised {e}. The buffer has been emptied.')
    pass
finally:
    return {
        "images": self.img_buffer,
        "gpio_data": self.gpio_buffer,
        "timestamps": self.timestamps_buffer,
    }
```