# ffmpeg-cheat-sheet

### Play an IP Camera Stream
```
ffplay "rtsp://username:password@192.168.0.102:554/abcd"
```

### Resize VIDEO
```
$ ffmpeg -i originalVideo.mov -vf scale=1080:-1 scaledVideo.mp4
```

### Push IP Cam RTSP stream to a RTMP server for distribution
```
$ ffmpeg -an -rtsp_transport tcp -i "rtsp://username:password@192.168.0.102:554/abcd" -tune zerolatency -vcodec libx264 -pix_fmt + -c:v copy -f flv -flvflags no_duration_filesize rtmp://123.0.0.1:1935/live/test
```

### Trim MP4 Meta Data
```
$ ffmpeg -i boring.mp4 -ss 00:00:03 -t 00:00:08 -async 1 focus.mp4
(ss: start_trim, t: duration, i: input video)
```

### Convert mp4 to GIF
```
$ ffmpeg -ss 0 -t 10 -i xn.mp4 -vf "fps=10,scale=640:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 xn.gif
```

### Check MP4 Meta Data
```
$ ffmpeg -i in.mp4 -c copy -map_metadata 0 -map_metadata:s:v 0:s:v -map_metadata:s:a 0:s:a -f ffmetadata in.txt
```

### Flip and Rotate Video 360
```
$ ffplay "rtsp://admin:123@19268.0.100:554/onvif1" -vf "transpose=3, transpose=2,format=yuv420p"
```

### Stream a MP4 Video to RTSP Server
```
$ ffmpeg -re -stream_loop -1 -i bodycam_08012022.mov -c copy -f rtsp rtsp://localhost:8554/mystream -b:v 2M -maxrate 2M -bufsize 1M
```

### List all wired Video and Audio capture devices
```
$ ffmpeg -f avfoundation -list_devices true -i ""
```

### Record Webcam to an mp4 files
```
$ ffmpeg -f avfoundation -framerate 30 -video_size 1280x960 -i "0:0" "../output.mp4"
```

### Record IP RTSP Stream to mp4 files
$ ffmpeg -i "rtsp://username:password@192.168.1.123:554/onvif1" "../recorded.mp4"
