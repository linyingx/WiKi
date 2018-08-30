Ubuntu16.04 安装openjdk-7-jdk 

sudo apt-get install openjdk-7-jre 或者sudo apt-get install openjdk-7-jdk

Ubuntu16.04的安装源已经默认没有openjdk7了，所以要自己手动添加仓库，如下：

### 1. oracle openjdk ppa source
```
sudo add-apt-repository ppa:openjdk-r/ppa
sudo apt-get update
sudo apt-get install openjdk-7-jdk  // OpenJdk 7安装：
```

### 2. oracle java jdk ppa source
```
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
```

JDK6 ：
```
sudo apt-get install oracle-java6-installer
```

JDK 7：
```
sudo apt-get install oracle-java7-installer
```

JDK 8:
```
sudo apt-get install oracle-java8-installer
```

如果安装成功之后还是不能用可能不有多个版本，选的不对
```
sudo update-alternatives --config java
sudo update-alternatives --config javac
```
选出正确的版本