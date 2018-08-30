Ubuntu添加开机启动脚本的方法
==

#### 1. 修改`rc.local`文件
`/etc/rc.local`文件内容如下
```
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.

exit 0
```
在`exit 0`之前加入自定义的内容即可

#### 2. 添加开机脚本
新建个脚本文件`new_service.sh`, 在`exit 0`之前写入具体命令

```
#!/bin/bash
# command content

exit 0
```
设置权限

```
sudo chmod 755 new_service.sh
```
把文件放到启动目录下

```
sudo mv new_service.sh /etc/init.d/
```
将自定义脚本添加到启动脚本

执行如下指令，在这里90表明一个优先级，越高表示执行的越晚
```
cd /etc/init.d/
sudo update-rc.d new_service.sh defaults 90
```

#### 移除Ubuntu开机脚本
```
sudo update-rc.d -f new_service.sh remove
```

