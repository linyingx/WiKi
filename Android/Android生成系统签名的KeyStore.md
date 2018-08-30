转自：https://blog.csdn.net/li411816761/article/details/52872554

下面来简单讲讲如何生成对应系统的系统签名:
```
1.android 源码目录build\target\product\security 取platform.pk8 platform.x509.pem放到一个目录下  
2 openssl pkcs8 -in platform.pk8 -inform DER -outform PEM -out shared.priv.pem -nocrypt//生成shared.priv.pem
3 openssl pkcs12 -export -in platform.x509.pem -inkey shared.priv.pem -out shared.pk12 -name androiddebugkey    //生成pkcs12
Enter Export Password: (输入密码android，默认是android，如是自己制作的key，输入对应的密码)
Verifying - Enter Export Password:(输入密码android)
4 生成debug.keystore
keytool -importkeystore -deststorepass android -destkeypass android -destkeystore debug.keystore -srckeystore shared.pk12 -srcstoretype PKCS12 -srcstorepass android -alias androiddebugkey
5. keytool -importkeystore -srckeystore debug.keystore -destkeystore debug.keystore -deststoretype pkcs12 //使用以上命令迁移到行业标准格式 PKCS12
```