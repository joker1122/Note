* [ADB](#ABD)
  * [常用指令](#常用指令)
  * [查看设备信息](#查看设备信息)
  * [查看日志](#查看日志)
  * [与应用交互](#与应用交互)
  * [控制电源与网络](#控制电源与网络)
  * [实用功能](#实用功能)
  * [可能遇到的问题](#可能遇到的问题)

## ADB
> ADB全称是Android Debug Bridge，是PC端与Android系统的通信工具。通过它可以在PC端操作  
Android 的文件系统

### 常用指令
* adb [-d|-e|-s <serialNumber\>] <command\>
> -d: 指定当前唯一通过USB连接的设备为命令目标  
> -e: 指定当前唯一运行的模拟器为命令目标  
> -s: 通过 **serialNumber** 指定命令目标  
> 若只有一台设备则直接使用 **adb <command\>** 即可
* adb devices
> 用于查看已连接到PC端的设备
* adb connect [serialNumber]
> 用于连接指定的设备，serialNumber可使用 **adb devices** 查看。如若遇到多台设备则可以使用  
> **adb -s <serialNumber\>** 来指定某一设备
- adb kill-server
> 用于停止 adb server
- adb start-server
> 用于开启 adb server， 一般执行adb命令会自动开启
- adb remount
> 将Android的文件系统重新挂载，这样就可以对Android的文件系统进行读写操作
- adb shell
> 打开Android系统的shell工具，可以使用各种命令来操作Android的文件系统
* adb push <PathFrom\> <PathTo\>
> 将PC端指定目录的文件推到Android文件系统指定目录
* adb pull <PathFrom\> <PathTo\>
> 将Android文件系统指定目录的文件推到PC端指定目录
* adb install [-l | -r | -t | -s | -d | -g] <Path\>
> 通过APK的绝对路径将APK安装到Android端
>> 1. -l : 将应用安装到保护目录 /mnt/asec  
>> 2. -r ：允许覆盖安装
>> 3. -t ： 允许安装 AndroidManifest.xml 里 application 指定 android:testOnly="true"   的应用
>> 4. -s ： 将应用安装到 sdcard
>> 5. -d ： 允许降级覆盖安装
>> 6. -g ： 授予所有运行时权限
* adb uninstall [-k] <packagename\>
> 通过包名来卸载指定程序,***-k*** 可选参数表示卸载应用但保留数据和缓存目录
* adb shell pm list packages [-s|-3]
> 用于列出Android端已安装程序的包名
>> * -s:列出系统程序包名
>> * -3:列出非系统程序包名
* adb shell pm path <Package\>
> 通过包名查看应用的安装路径
* adb shell pm clear <packagename\>
> 清楚应用的数据与缓存
### 查看设备信息
* adb shell ifconfig
> 查看网络信息
* adb shell getprop ro.product.model
> 查看设备型号
* adb shell dumpsys battery
> 查看电池状况
* adb shell wm size
> 查看屏幕分辨率，在后面加参数可修改设备分辨率，如：***adb shell wm size 480x1024***
* adb shell wm density
> 查看屏幕密度，在后面加参数可修改设备屏幕密度，如：***adb shell wm density 160***
* adb shell dumpsys window displays
> 显示屏幕参数
* adb shell getprop ro.build.version.release
> 输出Android系统版本
* adb shell cat /proc/cpuinfo
> 获取CPU信息
* adb shell cat /proc/meminfo
> 查看内存信息
* adb shell wm overscan [Left] [Top] [Right] [Bottom]
> 设置显示区域，四个参数代表距各边的像素，可使用 ***adb shell wm overscan reset*** 恢复原显示
### 查看日志
> Android 系统的日志分为两部分，底层的 Linux 内核日志输出到 /proc/kmsg，Android 的日志输出到 /dev/log。
* adb logcat [<option\>] ... [<filter-spec\>] ...
> 命令格式，option设置输出模式，filter-spec设置过滤模式
* adb logcat -s [tag]
> 按Tag标签打印log
* adb logcat >[path]
> 将log输出到指定文件
* adb logcat [Tag]:[Level]
> 输出指定Tag,指定等级的log 如：***adb logcat joker:D***
* adb logcat -c
> 清空日志
* adb shell dmesg
> 输出Linux内核日志
### 与应用交互
> 主要使用 ***adb shell am <command\>*** 与应用交互
* adb shell am start [options] <INTENT\>
> 启动 ***INTENT*** 指定的Activity，如:***adb shell am start -n com.tencent.mm/.ui.LauncherUI***  
>> options:  
>> * -n:指定完整 component 名，用于明确指定启动哪个 Activity
>> * -c:指定 category
>> * -a:指定Action
* adb shell am startservice [options] <INTENT\>
> 启动 ***INTENT*** 指定的Service
* adb shell am broadcast [options] <INTENT\>
> 发送 ***INTENT*** 指定的广播
* adb shell am force-stop <packagename\>
> 强制停止与 ***packagename*** 相关的进程
### 控制电源与网络
> 主要使用/system/bin 目录下的svc命令
* adb shell svc power stayon [true|false|usb|ac]
> 设置屏幕的常亮，true保持常亮，false不保持，usb当插入usb时常亮，ac当插入电源时常亮  
* adb shell svc data disable
> 关闭数据连接
* adb shell svc data enable
> 开启数据连接
* dab shell svc data prefer
> 设置数据连接优先于wifi
* adb shell svc wifi disable
> 关闭wifi
* adb shell svc wifi enable
> 开启wifi
* dab shell svc wifi prefer
> 设置wifi优先于数据连接
### 实用功能
* adb shell screencap -p /sdcard/sc.png
> 截屏并保存到设备指定目录
* adb shell screenrecord /sdcard/filename.mp4
> 录制屏幕并保存到指定目录，可按 ***Ctrl+c*** 停止
* > adb shell  
> su  
> cat /data/misc/wifi/\*.conf
>> wifi信息保存在 ***/data/misc/wifi/\*.conf*** 文件里，可通过以上命令查看，但需要超级用户权限
* adb shell monkey <command\>
> 使用 ***monkey*** 命令对程序做压力测试
> * -v : 指定反馈级别  
> * -p <packagename\> : 指定测试的包名,可指定多个包
> * -s : 用于指定伪随机数的生成种子
> * --throttle <毫秒\> : 用于指定事件间的时延  
* adb shell input [<source\>] <command\> [<arg\>...]
> 用于模拟按键或输入,如：***adb shell input keyevent 26*** 相当于按下电源键  
***adb shell input text joker*** 相当于往输入框输入 ***joker***
### 可能遇到的问题
* adb connect [serialNumber]连接不上
> 1. Android端的adbd服务没打开，可通过串口连接设备，在 ***root*** 权限下执行***start adbd    ***  开启服务
> 2. 提示多台设备，但只连了一台设备，依次执行 ***adb kill-server***，***adb start-server***
* adb install 安装程序失败
> 1. 没有挂载，执行 ***adb remount*** 挂载Android文件系统。
> 2. 相同包名程序存在，可使用 ***adb unimstall <packagename\>*** 通过包名卸载再安装，或使用  
***adb install -r <Path\> *** 覆盖。
