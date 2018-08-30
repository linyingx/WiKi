### JNI编程-- undefined reference to `__android_log_print' 的解决办法

按如下步骤操作：

1、在android.mk 文件中找到

```
include $(CLEAR_VARS)  这一行，
```

在下面增加一行：
```
LOCAL_LDLIBS    := -lm -llog 
```

2、文件头部引入：

```
#include <android/log.h>
```

3、宏定义

```
#define LOG_TAG "Native"

#define LOGE(...) __android_log_print(ANDROID_LOG_ERROR,LOG_TAG,__VA_ARGS__)
```