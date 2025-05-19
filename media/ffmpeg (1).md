# ffmpeg

{% embed url="https://linux.die.net/man/1/ffmpeg" %}



**Convert from `.mov` to `.mp4`**

> -vcodec _codec_
>
> Force video codec to _codec_. Use the "copy" special value to tell that the raw codec data must be copied as is.

> -acodec _codec_
>
> Force audio codec to _codec_. Use the "copy" special value to specify that the raw codec data must be copied as is.

```bash
$ ffmpeg -i [file_to_convert].mov -vcodec libx264 -acodec aac [output_file_name].mp4
```



**Extract portion of  video**

Eg. Extract video portion from 10 minutes 05 seconds to 10 minutes 20 seconds (15 seconds video length from `-t` flag) from **test.mp4**, and store to output file **output.mp4**.

```
$ ffmpeg -ss 00:10:05 -t 00:00:15 -i 'test.mp4' -vcodec copy -acodec copy output.mp4
```
