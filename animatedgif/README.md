### Animated Gif

#### How to screen capture

Quicktime Player

```
File ---> New Screen Recording
```

#### Convert mov to gif

```
ffmpeg -i /Users/seita/Desktop/injection_site_filter.mov -pix_fmt rgb24 /Users/seita/Desktop/injection_site_filter.gif

ffmpeg -ss 00:00:00.000 -i /Users/seita/Desktop/injection_site_filter.mov -pix_fmt rgb24 -r 10 -s 320x240 -t 00:00:11.000 /Users/seita/Desktop/injection_site_filter.gif

ffmpeg -ss 00:00:00.000 -i /Users/seita/Desktop/injection_site_filter.mov -pix_fmt rgb24 -r 10 -s 750x460 -t 00:00:11.000 /Users/seita/Desktop/injection_site_filter_750_460.gif

ffmpeg -ss 00:00:00.000 -i /Users/seita/Desktop/injection_site_filter.mov -pix_fmt rgb24 -r 10 -s 1432x788 -t 00:00:11.000 /Users/seita/Desktop/injection_site_filter2.gif
```
