### 使用adb更改系统参数

![图片](Picture/37129019.png)

settings命令不需要权限就可以执行。
这个命令设置的是Setting provider的值，其key和namespace的值定义在如下文件中：
frameworks/base/core/java/android/provider/Settings.java

如下图就是namespace global的定义，其它的定义类似。
![图片](Picture/37306210.png)