---
layout: post
title: 使用ffmpeg进行视频剪辑处理（初级）
category: study
description: 使用ffmpeg批量减掉片头或片尾指定长度的视频
tags:
- 学习笔记
- ffmpeg
- 视频处理
- 批处理
---

前几日，同事需要批量处理一些视频文件。需求是将众多视频的前面5秒和后面10秒删去。本来只会用现成图形化软件的我，听说有ffmpeg这等神奇，很是好奇。

初研究了一下，用ffmepg在视频前面删除固定长度是非常方便的，因为提供了直接就可以使用的参数。但是要批量截去视频结尾固定长度的视频，却比较棘手。

网络上提供的版本无一不是先用ffprobe返回视频的长度，然后将该长度减去固定时长，作为参数再返回给ffmpeg调用。第一种实现方式如下：

```bat
@echo off && setlocal enabledelayedexpansion
set _sof=5
::_sof代表StartOfFile 默认为5秒
set _eof=5
::_eof代表EndOfFile 默认为5秒
set targetFolder="d:\croppedMovies"
::targetFoler代表最终的输出文件夹，请确保先在这个位置建立这个文件夹
for /f "delims=" %%i in ('dir /b /a-d /s "*.wmv"') do (ffprobe -show_entries format=duration -i "%%i" -v quiet -of csv="p=0">tmp
set /p _dur=<tmp
del tmp
echo !_dur!
set /a "_dur-=%_sof%"
set /a "_dur-=%_eof%"
echo !_dur!
ffmpeg -i "%%i" -ss %_sof% -t !_dur! -c copy "%targetFolder%\%%~nxi"
)
pause
```

上述代码在两台机器上测试均未发生问题，但在需用的同事那台机器上却报错了。至今原因未明。

另外一种方法是技术大拿提供的。该方法是先写好针对一个视频的批处理文件，然后要批量剪辑的时候，再用循环来调用这个批处理文件。

例如，将处理单个视频的批处理文件保存为cut.bat文件，代码如下：

```bat
@echo off
for /f "tokens=*" %%a in ('ffprobe -show_format -i %1 ^| find "duration"') do set _duration=%%a
set _duration=%_duration:~9%
for /f "delims=. tokens=1*" %%b in ('echo %_duration%') do set /a "_durS=%%b"
for /f "delims=. tokens=2*" %%c in ('echo %_duration%') do set "_durMS=%%c"
set /a "_durS-=%4"
set /a "_durS-=%3"
set "_newduration=%_durS%.%_durMS%"
set "_output=%~n1"
ffmpeg -y -i %1 -ss %3 -t %_newduration% -c copy %2
```

将该文件与ffmpeg和ffprobe都放到含有视频的文件夹中，然后再在这个文件夹中生成如下循环各个文件的批处理：

```bat
@echo off
::要实现创建输出目录，例如 E:\work\croppedmovies\
::下一行最后两个参数5、10分别代表片头或片尾要裁掉的长度，可以自行修改
for /f "delims=" %%i in ('dir /b /a-d /s "*.wmv"') do cut "%%i" "E:\work\croppedmovies\%%~ni.wmv" 5 10
pause
```

然后运行上面这个文件即可。

另外，该技术达人提供了批量为视频添加片头的批处理代码，也记录在这里：

```bat
@echo off
for /f "delims=" %%i in ('dir /b /a-d /s "*.mp4"') do ffmpeg -y -i 片头.mp4 -i "%%i" -filter_complex "[0:v:0] [0:a:0] [1:v:0] [1:a:0] concat=n=2:v=1:a=1 [v] [a]" -map "[v]" -map "[a]" -c:v libx264 -preset fast -b:v 800k -maxrate 5000k -c:a aac -b:a 96k  "E:\work\croppedmovies\%%~ni.mp4"
pause
```
