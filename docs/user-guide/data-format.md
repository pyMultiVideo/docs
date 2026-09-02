# Data format

When video is recorded data files are saved in the data directory specified in the Video Capture tab.  Video filenames are given by the subject ID and recording start date-time.  Each recording creates three data files:

- The video file (.mp4)
- Metadata file (.json)
- Frame info file (.csv)

The video file is a standard .mp4 video encoded using either the h264 or h265 video compression standard depending on the FFMPEG settings.

The metadata file contains information about the recording as shown in this example:

```
{
    "subject_ID": "test",
    "camera_unique_id": "20073102-spinnaker",
    "camera_name": "chameleon",
    "FPS": 60,
    "exposure_time": 6451,
    "gain": 0,
    "pixel_format": "mono8",
    "device_model": "Chameleon3 CM3-U3-13Y3M",
    "device_serial_number": "20073102",
    "start_time": "2026-07-29T15:40:53.965",
    "end_time": "2026-07-29T15:40:57.573",
    "duration": "0:00:03.608",
    "recorded_frames": 214,
    "dropped_frames": 0,
    "camera_buffer_overflow": false,
    "ffmpeg_buffer_overflow": false,
    "downsampling_factor": 1,
    "compression_standard": "h264",
    "encoding_speed": "fast",
    "encoding_crf": 28
}
```

The frame info file contains frame numbers, the state of the camera GPIO pins and frame timestamps in microseconds since the start of the recording.  Each row corresponds to one frame of the video file, with a one line header indicating the column names, as seen in this example:

```csv
number,GPIO1,GPIO2,GPIO3,timestamp
1,1,1,0,0
2,1,1,0,16654
3,1,1,0,33313
4,1,1,0,49965
5,1,1,0,66618
6,1,1,0,83276
7,1,1,0,99927
...
```

