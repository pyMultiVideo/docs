# Data format

Once you have successfully recorded video the data will recorded to the /data folder, unless otherwise specificed.

Each recording will have three files associated with that recording session.

- The video file (.mp4)
- Metadata file (.json)
- GPIO pinstates file (.csv)

The metadata file gives recording information about the video recorded.

GPIO pinstates file has the following file format:

```csv
GPIO1,GPIO2,GPIO3,Timestamp
1,1,0,000000000000000
1,1,0,000000014277142
1,1,0,000000028554282
1,1,0,000000042827719
...
```

Each of the `GPIO1`, `GPIO2`, `GPIO3` columns correspond to the pinstates of a given frame and the `Timestamp` corresponds to the time since the recording began of the frame being recorded.

The length of this file is the same length as the number of frames recorded from the `.mp4` video file.
