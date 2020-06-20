---
title: B站视频缓存，导出
date: 2020-06-20 18:02:30
tags:
---

### Android 缓存 B 站视频

Android 手机存储位置 `/sdcard/Android/data/tv.danmaku.bili/download`

导出视频信息
adb pull /sdcard/Android/data/tv.danmaku.bili/download

### 安装 ffmpeg

`brew install ffmpeg`

```
 # ffmpeg --version
ffmpeg version 4.2.3 Copyright (c) 2000-2020 the FFmpeg developers
  built with Apple clang version 11.0.3 (clang-1103.0.32.59)
  configuration: --prefix=/usr/local/Cellar/ffmpeg/4.2.3_1 --enable-shared --enable-pthreads --enable-version3 --enable-avresample --cc=clang --host-cflags=-fno-stack-check --host-ldflags= --enable-ffplay --enable-gnutls --enable-gpl --enable-libaom --enable-libbluray --enable-libdav1d --enable-libmp3lame --enable-libopus --enable-librubberband --enable-libsnappy --enable-libsrt --enable-libtesseract --enable-libtheora --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwebp --enable-libx264 --enable-libx265 --enable-libxvid --enable-lzma --enable-libfontconfig --enable-libfreetype --enable-frei0r --enable-libass --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libopenjpeg --enable-librtmp --enable-libspeex --enable-libsoxr --enable-videotoolbox --disable-libjack --disable-indev=jack
  libavutil      56. 31.100 / 56. 31.100
  libavcodec     58. 54.100 / 58. 54.100
  libavformat    58. 29.100 / 58. 29.100
  libavdevice    58.  8.100 / 58.  8.100
  libavfilter     7. 57.100 /  7. 57.100
  libavresample   4.  0.  0 /  4.  0.  0
  libswscale      5.  5.100 /  5.  5.100
  libswresample   3.  5.100 /  3.  5.100
  libpostproc    55.  5.100 / 55.  5.100
Unrecognized option '-version'.
Error splitting the argument list: Option not found
```

### 合成视频

查看 每个视频 缓存信息

```
 #xxxxx/220  tree
.
├── 64
│   ├── audio.m4s
│   ├── index.json
│   └── video.m4s
├── danmaku.xml
└── entry.json

1 directory, 5 files
```

#### 查看文件 video.m4s 内容
```
 #/64  ffprobe -print_format json video.m4s
ffprobe version 4.2.3 Copyright (c) 2007-2020 the FFmpeg developers
  built with Apple clang version 11.0.3 (clang-1103.0.32.59)
  configuration: --prefix=/usr/local/Cellar/ffmpeg/4.2.3_1 --enable-shared --enable-pthreads --enable-version3 --enable-avresample --cc=clang --host-cflags=-fno-stack-check --host-ldflags= --enable-ffplay --enable-gnutls --enable-gpl --enable-libaom --enable-libbluray --enable-libdav1d --enable-libmp3lame --enable-libopus --enable-librubberband --enable-libsnappy --enable-libsrt --enable-libtesseract --enable-libtheora --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwebp --enable-libx264 --enable-libx265 --enable-libxvid --enable-lzma --enable-libfontconfig --enable-libfreetype --enable-frei0r --enable-libass --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libopenjpeg --enable-librtmp --enable-libspeex --enable-libsoxr --enable-videotoolbox --disable-libjack --disable-indev=jack
  libavutil      56. 31.100 / 56. 31.100
  libavcodec     58. 54.100 / 58. 54.100
  libavformat    58. 29.100 / 58. 29.100
  libavdevice    58.  8.100 / 58.  8.100
  libavfilter     7. 57.100 /  7. 57.100
  libavresample   4.  0.  0 /  4.  0.  0
  libswscale      5.  5.100 /  5.  5.100
  libswresample   3.  5.100 /  3.  5.100
  libpostproc    55.  5.100 / 55.  5.100
{
Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'video.m4s':
  Metadata:
    major_brand     : iso5
    minor_version   : 1
    compatible_brands: avc1iso5dsmsmsixdash
    encoder         : Lavf57.71.100
    description     : Packed by Bilibili XCoder v2.0.2
  Duration: 00:12:09.05, start: 0.092000, bitrate: 157 kb/s
    Stream #0:0(und): Video: h264 (High) (avc1 / 0x31637661), yuv420p, 1280x720, 1 kb/s, 15 fps, 15 tbr, 16k tbn, 30 tbc (default)
    Metadata:
      handler_name    : VideoHandler

}
```

#### 查看文件 audio.m4s 内容
```
 # ffprobe -print_format json audio.m4s
ffprobe version 4.2.3 Copyright (c) 2007-2020 the FFmpeg developers
  built with Apple clang version 11.0.3 (clang-1103.0.32.59)
  configuration: --prefix=/usr/local/Cellar/ffmpeg/4.2.3_1 --enable-shared --enable-pthreads --enable-version3 --enable-avresample --cc=clang --host-cflags=-fno-stack-check --host-ldflags= --enable-ffplay --enable-gnutls --enable-gpl --enable-libaom --enable-libbluray --enable-libdav1d --enable-libmp3lame --enable-libopus --enable-librubberband --enable-libsnappy --enable-libsrt --enable-libtesseract --enable-libtheora --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwebp --enable-libx264 --enable-libx265 --enable-libxvid --enable-lzma --enable-libfontconfig --enable-libfreetype --enable-frei0r --enable-libass --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libopenjpeg --enable-librtmp --enable-libspeex --enable-libsoxr --enable-videotoolbox --disable-libjack --disable-indev=jack
  libavutil      56. 31.100 / 56. 31.100
  libavcodec     58. 54.100 / 58. 54.100
  libavformat    58. 29.100 / 58. 29.100
  libavdevice    58.  8.100 / 58.  8.100
  libavfilter     7. 57.100 /  7. 57.100
  libavresample   4.  0.  0 /  4.  0.  0
  libswscale      5.  5.100 /  5.  5.100
  libswresample   3.  5.100 /  3.  5.100
  libpostproc    55.  5.100 / 55.  5.100
{
Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'audio.m4s':
  Metadata:
    major_brand     : iso5
    minor_version   : 1
    compatible_brands: avc1iso5dsmsmsixdash
    encoder         : Lavf57.71.100
    description     : Packed by Bilibili XCoder v2.0.2
  Duration: 00:12:09.11, start: 0.000000, bitrate: 97 kb/s
    Stream #0:0(und): Audio: aac (LC) (mp4a / 0x6134706D), 44100 Hz, stereo, fltp, 0 kb/s (default)
    Metadata:
      handler_name    : SoundHandler

}
```


#### 使用 java 进行 合成

```java
import com.alibaba.fastjson.JSONObject;
import javafx.util.Pair;

import java.io.File;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.Arrays;
import java.util.List;
import java.util.concurrent.LinkedBlockingQueue;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;

public class CombineBilibiliViewo {

    public static void main(String[] args) {

        String srcCachePath = "100";
        String mp4OutputPath = "mp4";

        final File projectFolder = new File(srcCachePath);
        /* 获取到第一级目录 */
        final File[] files = projectFolder.listFiles(pathname -> !pathname.getName().contains(".DS_Store"));

        final ThreadPoolExecutor poolExecutor = new ThreadPoolExecutor(
                1,
                4,
                30, TimeUnit.SECONDS,
                new LinkedBlockingQueue<>(files.length));

        Arrays.asList(files)
                .stream()
                .forEach(file -> {

                    poolExecutor.submit(() -> {
                        try {
                            final File entity = new File(file, "entry.json");
                            final Pair<String, String> pair = getFileNameFromEntryJson(entity.getAbsolutePath());
                            String fileName = pair.getValue();
                            final String typeTag = pair.getKey();

                            final String videoPath = file.getAbsolutePath();
                            String audioM4s = videoPath + File.separator + typeTag + File.separator + "audio.m4s";
                            String videoM4s = videoPath + File.separator + typeTag + File.separator + "video.m4s";
                            String targetFilePath = mp4OutputPath + File.separator + fileName.replaceAll(" ", "-");
                            combineVideo(file.getName(), audioM4s, videoM4s, targetFilePath);
                        } catch (Exception e) {
                            System.err.println(e.getMessage());
                        }
                    });

                });

        poolExecutor.shutdown();

    }

    private static Pair<String, String> getFileNameFromEntryJson(String absolutePath) {
        try {
            final List<String> strings = Files.readAllLines(Paths.get(absolutePath), StandardCharsets.UTF_8);
            final String content = String.join("", strings);
            final JSONObject parse = (JSONObject) JSONObject.parse(content);
            final String typeTag = parse.getString("type_tag");
            final JSONObject pageData = parse.getJSONObject("page_data");
            final String part = pageData.getString("part");
            return new Pair(typeTag, part);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return null;
    }

    public static boolean isFileExists(String filePath) {
        final File file = new File(java.lang.String.valueOf(filePath));
        if (file.exists() && file.isFile()) {
            return true;
        }
        return false;
    }

    private static void combineVideo(String index, String audioM4s, String videoM4s, String destFilePath) {
        if (!isFileExists(audioM4s)) {
            throw new RuntimeException("文件不存在:" + audioM4s);
        }
        if (!isFileExists(videoM4s)) {
            throw new RuntimeException("文件不存在:" + videoM4s);
        }
        try {
            final String command = String.format("ffmpeg -i %s -i %s -vcodec copy -acodec copy %s.mp4", audioM4s, videoM4s, destFilePath);
            Runtime.getRuntime().exec(command);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```


### 查看 合并完成后的文件信息
```
 # ffprobe -print_format json xxx.mp4
ffprobe version 4.2.3 Copyright (c) 2007-2020 the FFmpeg developers
  built with Apple clang version 11.0.3 (clang-1103.0.32.59)
  configuration: --prefix=/usr/local/Cellar/ffmpeg/4.2.3_1 --enable-shared --enable-pthreads --enable-version3 --enable-avresample --cc=clang --host-cflags=-fno-stack-check --host-ldflags= --enable-ffplay --enable-gnutls --enable-gpl --enable-libaom --enable-libbluray --enable-libdav1d --enable-libmp3lame --enable-libopus --enable-librubberband --enable-libsnappy --enable-libsrt --enable-libtesseract --enable-libtheora --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwebp --enable-libx264 --enable-libx265 --enable-libxvid --enable-lzma --enable-libfontconfig --enable-libfreetype --enable-frei0r --enable-libass --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libopenjpeg --enable-librtmp --enable-libspeex --enable-libsoxr --enable-videotoolbox --disable-libjack --disable-indev=jack
  libavutil      56. 31.100 / 56. 31.100
  libavcodec     58. 54.100 / 58. 54.100
  libavformat    58. 29.100 / 58. 29.100
  libavdevice    58.  8.100 / 58.  8.100
  libavfilter     7. 57.100 /  7. 57.100
  libavresample   4.  0.  0 /  4.  0.  0
  libswscale      5.  5.100 /  5.  5.100
  libswresample   3.  5.100 /  3.  5.100
  libpostproc    55.  5.100 / 55.  5.100
{
Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'xxxx.mp4':
  Metadata:
    major_brand     : isom
    minor_version   : 512
    compatible_brands: isomiso2avc1mp41
    encoder         : Lavf58.29.100
    description     : Packed by Bilibili XCoder v2.0.2
  Duration: 00:31:25.88, start: 0.000000, bitrate: 333 kb/s
    Stream #0:0(und): Video: h264 (High) (avc1 / 0x31637661), yuv420p, 1280x720, 233 kb/s, 15 fps, 15 tbr, 16k tbn, 30 tbc (default)
    Metadata:
      handler_name    : VideoHandler
    Stream #0:1(und): Audio: aac (LC) (mp4a / 0x6134706D), 44100 Hz, stereo, fltp, 96 kb/s (default)
    Metadata:
      handler_name    : SoundHandler

}
```

