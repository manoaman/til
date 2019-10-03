### Animated Gif

#### How to screen capture

Quicktime Player

```
File ---> New Screen Recording
```

#### Convert mov to gif

```
ffmpeg -i file.mov -pix_fmt rgb24 file.gif

ffmpeg -ss 00:00:00.000 -i file.mov -pix_fmt rgb24 -r 10 -s 320x240 -t 00:00:11.000 file.gif

ffmpeg -ss 00:00:00.000 -i file.mov -pix_fmt rgb24 -r 10 -s 750x460 -t 00:00:11.000 file_750_460.gif

ffmpeg -ss 00:00:00.000 -i file.mov -pix_fmt rgb24 -r 10 -s 1432x788 -t 00:00:11.000 file2.gif
```
