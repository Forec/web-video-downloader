# Web Video Downloader （在线视频下载工具）
> This project is a spider-like tool for **downloading videos in browser** . For example, I want to download one of my favourite cartoons named 《Zombie Cats》, it can be found in bilibili, url is [http://www.bilibili.com/video/av6376703/](http://www.bilibili.com/video/av6376703/). Three ways for you to download the video, register in bilibili, use fiddler(or other softwares) to capture the address of video, or use my tool.

## Platform
This small script is written in python 3.5, using some easy-install packages, all listed below.
* built-in packages : `os`, `time`, `requests`, `argparse`, `threading`.
* **selenium** : You can install by `pip3 install selenium`.
* **browsermob-proxy** : You can install by `pip3 install browsermob-proxy`. Then, download `browsermob-proxy` from [here](https://github.com/downloads/webmetrics/browsermob-proxy/browsermob-proxy-2.0-beta-6-bin.zip), add its `bin` path to environment `PATH` variable. You can see there're two files `browsermob-proxy` and `browsermob-proxy.bat` in directory `bin`.
* **Firefox** : This tool needs firefox. Remember to **add your firefox path to environment variable**, or you need to specify where firefox is when you execute this tool. However, other browsers like Chrome, Opera, etc, are also supported, and you need to install some plugins. I didn't test them, so I will not show how to configure, but search `selenium chrome driver` may help you. If you have firefox, check your version. My firefox is FF48( the latest version) . I suggest you followed my introduction to install **FF48**, since firefox is the easiest way to configure.
* **wires** : This is a plugin designed by firefox team, which is used to support `selenium`, you can download it from [here](https://github.com/mozilla/geckodriver/releases), make sure that the `geckodriver` is version 0.9, **DONT USE 0.10** if you use FF47 or later versions, because there's a bug related. The detail about this bug is [here](https://github.com/mozilla/geckodriver/issues/154). After you download this `zip` file, unzip it, and you will get onefile `geckodriver.exe`. **Rename it to `wires.exe`, and put it under the same directory with my tool.**

## EXPLANATION
* This tool use `selenium` to **simulate your actions**. For example, you want to download `Zombie Cats`, give a url to this tool, it will open your browser, just like what you do if you want to watch it online. However, it will parse all the links created in the period loading the page, and get the most probably url for the real video. Since most of websites do not set their videos to a permanent link, it's hard to get the real link to videos using tranditional spiders. I use `browsermob-proxy`, which redirects the data flow to a monitor. After assigned waiting-time, the tool will close the browser and start downloading all the videos found in page. So the **waiting-time is important**, if you give a short time, like `1s`, the real video link may not be received yet.
* For FF47 and later versions, `selenium` needs `DesiredCapabilities` to start firefox, in code, they are line 46 to line 49.
* My tool only search urls containing `mp4`, `flv`, `avi`, `rmvb` and `rm`. If you want to contain more suffixs, modify line 40 or line 88. I didn't provide any parameter  for suffixs because you can add more suffixs when you create the `Simulator` object.

## Usage
Just run `python3 video_capture.py <parameters>`. Videos will be downloaded into folder `download`, and renamed by their numbers. Also, you can download the executable binary file `video_capture.exe` from my cloud storage: [here](http://7xktmz.com1.z0.glb.clouddn.com/video_capture.exe). The parameters are:
* --url: the url for the page which contains your target video.
* --time: the **WAITING TIME**, that is, when this tool open your browser, how much time will the browser alive. Which is also the time my tool capture urls. I suggest you use default, which is `30s`. It depends on websites. `bilibili` needs no more than `10s`, but `youku` may need `60s`, since its advertisements are already `45s`, after these advertisements, the server sends real link for video.
* --bin: the path to your `firefox.exe`, if you have configured the `PATH` variable, this parameter is not required.
* --proxy: the path to your `browsermob-proxy.bat`, if you have configured the `PATH` variable, this parameter is not required.
* **ATTENTIONS** : This tool can easily download videos in `Bilibili`, but for `youku` or other websites, their servers **cut a video into several pieces** , so my tool will receive theses pieces. **In such condition, I suggest you should not use this tool**, since these pieces must be combined to a complete video, but my tool doesn't support this function. Also, to get these pieces' links, you must set WAITING TIME a large number. That's annoying.
* Example: `video_capture.exe --url=http://www.bilibili.com/video/av6376703/ --time=10 --bin=C:\Firefox\firefox.exe --proxy=C:\browsermob-proxy-2.0-beta-6\bin\browsermob-proxy.bat`, this command will download `Zombie Cats 51` into folder `download`. In this example, I didn't configure my `PATH` variable, so I need to assign where firefox is and where `browsermob-proxy.bat` is. Here `time` is 10, so after 10 seconds, the tool will download the video.

## Update-logs
* 2016-9-23: Add this project.
* 2016-10-6: Rename and build repository.

# License
All codes in this repository are licensed under the terms you may find in the file named "LICENSE" in this directory.