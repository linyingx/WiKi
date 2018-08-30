Ubuntu14.04安装gollum
==

gollum github 上的安装指南如下:

### Ubuntu 14.04
```
sudo apt-get install ruby1.9.1 ruby1.9.1-dev make zlib1g-dev libicu-dev build-essential git cmake
sudo gem install gollum
```

但是安装时出现如下错误
```
Error installing gollum:
    mime-types-data requires Ruby version >= 2.0.
```

卸载 Ruby1.9.1
```
sudo apt remove ruby1.9.1 ruby1.9.1-dev
```

#### 安装更高版本Ruby
添加ruby的ppa源并更新
```
sudo add-apt-repository ppa:brightbox/ruby-ng
sudo apt-get update
```

安装`ruby2.3`
```
sudo apt-get install ruby2.3 ruby2.3-dev

```

尝试安装`mime-types-data`
```
sudo gem install mime-types-data
```
成功

安装`gollum`, 这个时间有点长.
```
sudo gem install gollum
```
安装完成,执行`gollum --v`显示
```
Gollum 4.1.2
```
安装成功

#### 使用`gollum`
可以把gollum和github结合起来使用很方便.
```
git clone https://github.com/linyingx/WiKi.git
cd Wiki
gollum
```
在浏览器里输入`http://localhost:4567`

#### 开机启动`gollum`
在文件`/etc/rc.local`中`exit 0`之前加入如下代码
```
# Git项目所在目录
cd ~/wiki
gollum &> /dev/null &
cd -
```

#### `gollum`不支持中文标题

##### 1. 文件名为中文的文件提交后在Files界面无法显示
执行`git status`发现文件名为乱码
```
# 中文的文件名会显示成下面的方式
vim\344\270\255\344\275\277\347\224\250markdown.md
```
解决方法:
```
git config --global core.quotepath false
```

##### 2. 无法建立中文名的文件
安装`gollum-rugged_adapter`, 运行`gollum时`, 加上参数`--adapter` 为`rugged`
```
sudo apt-get -y install cmake
sudo gem install gollum-rugged_adapter

gollum --port 80 --adapter rugged
```
安装`cmake`失败提示
```
下列软件包有未满足的依赖关系：
 cmake : 依赖: cmake-data (>= 2.8.12.2)
E: 无法修正错误，因为您要求某些软件包保持现状，就是它们破坏了软件包间的依赖关系。
```
根据提示先安装依赖, 再安装cmake:
```
sudo apt-get install cmake-data
sudo apt-get -y install cmake
```
接着安装`gollum-rugged_adapter`,依然错误提示
```
Could NOT find OpenSSL, try to set the path to OpenSSL root folder in the system variable OPENSSL_LIBRARIE(missing:  OPENSSL_LIBRARIE)
```
执行
```
sudo apt-get install libssl-dev
```
再次安装`gollum-rugged_adapter`成功. 
结束掉之前启动的gollum，带上参数再次启动中文不支持问题解决
