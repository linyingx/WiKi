系统原先安装有java8， 手动安装了java7后将其安装到update-alternatives里，
java8 的 priority 为 1081
`sudo update-alternatives --install /usr/bin/java java /opt/jdk1.7.0_79/bin/java 1082`

使用如下命令不生效
`sudo update-alternatives --config java`

从网上找的该当说是把JAVA_HOME等相关环境变量注释， 找到如下两个文件有定义JAVA环境变量，里面的内容全注释
`/etc/profile.d/jdk.csh`
`/etc/profile.d/jdk.sh`

重新打开Terminal后JAVA_HOME已经是空的了，但java -version命令依然还是java8, 可以看到alternatives里的文件已经改变。
![图片.png](https://upload-images.jianshu.io/upload_images/8033130-dc1acf7f6199166f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
把能设置的都设置了，不过没用
![图片.png](https://upload-images.jianshu.io/upload_images/8033130-f0bcd1dcf1e20da2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
增加JAVA_HOME配置, 也不行
![图片.png](https://upload-images.jianshu.io/upload_images/8033130-c10ec2421497ff28.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
找到一个关于android-studio 里jre的环境变量配置，这个方法可以，需要重启电脑
![图片.png](https://upload-images.jianshu.io/upload_images/8033130-191d959910e4f8ca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
