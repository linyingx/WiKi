[developer.android.google.cn/](https://developer.android.google.cn/guide/)

android有两个overlay目录：
```
DEVICE_PACKAGE_OVERLAYS
PRODUCT_PACKAGE_OVERLAYS
```

PRODUCT_PACKAGE_OVERLAYS的优先级要高于DEVICE_PACKAGE_OVERLAYS，如果有相同的内容，优先级高的内容将会覆盖优先级低的内容。
可以定义多个overlays目录，需要用空格隔开。如果有多个目录，并且都包含同一资源的定义，那么将使用第一个定义的目录中的资源。

通过overlay机制可以修改以下类型的资源：

以下几类能够通过该机制定义：

(1)，Configurations (string, bool, bool-array)

(2)，Localization (string, string-array)

(3)，UI Appearance (color, drawable, layout, style, theme, animation)

(4)，Raw resources (audio, video, xml)