使用系统 ubuntu 14.04, 测试有效果
```
git config --global gui.encoding utf-8
git config --global i18n.commitencoding utf-8
git config --global i18n.logoutputencoding utf-8
```
设置后会被写到~/.gitconfig中

执行`git status`发现文件名为乱码
```
# 中文的文件名会显示成下面的方式
vim\344\270\255\344\275\277\347\224\250markdown.md
```
解决方法: 
```
git config --global core.quotepath false
```