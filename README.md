# ffmpeg gif audio visualizer
A crusty ffmpeg script to overlay a waveform over a gif.

Well slightly. Convert the gif to static frames first :smirk_cat:

```sh
ffmpeg -loop 1 -r 30 -i FRAMES%02d.png -i AUDIO.wav -t 140 -filter_complex \
"[1:a]showwaves=mode=cline:s=500x200:colors=#00CCCC:scale=sqrt[v];
[0][v]overlay=(W-w)/2:H-h-1:shortest=1,scale='iw-mod(iw,2)':'ih-mod(ih,2)',format=yuv420p[v];
[v]drawtext=text='SONG NAME HERE'
:fontcolor=#EEEE66@1.0:borderw=1:bordercolor=#00CCCC@1.0
:shadowx=4:shadowy=4:shadowcolor=#000000@0.5
:fontsize=22:fontfile=/PATHTOFONT.ttf:x=(w-text_w)/5
:y=(h-text_h)/7[out]" \
-r 30 -map "[out]" -map 1:a -movflags +faststart -r 30 -pix_fmt yuv420p output.mp4
```

## Result

![Example Output](https://raw.githubusercontent.com/discatte/ffmpeg_gif_audio_visualizer/main/script_example_output.png)
