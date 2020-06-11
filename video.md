## View webcam content with MPV

[Based on this issue](https://github.com/mpv-player/mpv/issues/4614#issuecomment-602697806)

```
mpv av://v4l2:/dev/video0
```

example with options:

```
mpv --demuxer-lavf-format=video4linux2 --demuxer-lavf-o-set=input_format=mjpeg av://v4l2:/dev/video0
```

