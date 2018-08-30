* [ADB](#ABD)
  * [常用指令](#常用指令)
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
* adb install [-lrtsdg] <Path\>
> 通过APK的绝对路径将APK安装到Android端
>> 1. -l : 将应用安装到保护目录 /mnt/asec  
>> 2. -r ：允许覆盖安装
>> 2. -t ： 允许安装 AndroidManifest.xml 里 application 指定 android:testOnly="true"   的应用
>> 2. -s ： 将应用安装到 sdcard
>> 2. -d ： 允许降级覆盖安装
>> 2. -g ： 授予所有运行时权限
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
* adb shell wm density
> 获取设备的屏幕密度
* adb shell wm size
> 获取设备的分辨率
### 可能遇到的问题
* adb connect [serialNumber]连接不上
> 1. Android端的adbd服务没打开，可通过串口连接设备，在 ***root*** 用户下执行***start adbd    ***  开启服务
> 2. 提示多台设备，但只连了一台设备，依次执行 ***adb kill-server***，***adb start-server***
* adb install 安装程序失败
> 1. 没有挂载，执行 ***adb remount*** 挂载Android文件系统。
> 2. 相同包名程序存在，可使用 ***adb unimstall <packagename\>*** 通过包名卸载再安装，或使用  
***adb install -r <Path\> *** 覆盖。
