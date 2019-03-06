# Alfred_Youtube_Safari_MP3
We can download any song playing in youtube website in Safari browser using the command "cmd shift m" using this workflow.

Note that we need to download `youtube-dl` and `ffmpeg` to use this workflow, which are already shipped with this github
repo. We can either use `youtube-dl` from this github repo or install it directly from thier official [website](https://rg3.github.io/youtube-dl/) using commands:
```
sudo wget https://yt-dl.org/downloads/latest/youtube-dl -O /usr/local/bin/youtube-dl

sudo chmod a+rx /usr/local/bin/youtube-dl
```

If we donwload the binary from official website we also need to change the file path binary in Alfred workflow.


# Usage
![](alfred_youtube_safari_mp3.png)


# Dependencies information:
- [youtube-dl](https://rg3.github.io/youtube-dl/)
- [ffmpeg](https://www.ffmpeg.org)
