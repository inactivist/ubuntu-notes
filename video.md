## ffmpeg 

- [Stream webcams to other computers using ffmpeg](http://4youngpadawans.com/stream-camera-video-and-audio-with-ffmpeg/)
- [low-latency UDP streaming with ffmpeg](https://stackoverflow.com/questions/21213895/how-to-stream-live-videos-with-no-latency-ffplay-mplayer-and-what-kind-of-wra/30754270#30754270)
- Build complex filter graphs in python with [ffmpeg-python](https://github.com/kkroening/ffmpeg-python)

## View webcam content with MPV

[Based on this issue](https://github.com/mpv-player/mpv/issues/4614#issuecomment-602697806)

```
mpv av://v4l2:/dev/video0
```

example with options:

```
mpv --demuxer-lavf-format=video4linux2 --demuxer-lavf-o-set=input_format=mjpeg av://v4l2:/dev/video0
```

