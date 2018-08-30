VIM中使用markdown
==
安装环境 Ubuntu 14.04 Vim 8

### vim-markdown插件
此插件用于markdown语法高亮

因为我使用的vimplug来管理插件,所以在`.vimrc`里加入如下代码

```
Plug 'plasticboy/vim-markdown'
```
之后执行

```
:PlugInstall
```

但是也不知道是什么原因,安装这个插件后并不能生效, 反而不安装的时候会有语法高亮.

### vim-instant-markdown插件
此插件用于markdown实时预览,据网上介绍安装完这个插件后用vim打开markdown文档的时候,
会自动打开一个浏览器窗口,并可以实时预览,并且支持滚动同步.

##### 安装此插件需要安装最新版本的`node.js`
```
sudo add-apt-repository ppa:chris-lea/node.js
sudo apt-get update
sudo apt-get install nodejs
```
##### 安装完`node.js`之后安装`instant-markdown-d`
```
sudo npm -g install instant-markdown-d
```
##### 安装vim-instant-markdown插件
```
Plug 'suan/vim-instant-markdown'
```
vim里执行:
```
:PluginInstall
```

但我安装完后打开`md`文档并不能自动打开浏览器,在网上找了一下也没有找到解决方案,
因此决定安装一个 `markdown-preview`

### markdown-preview插件
此插件支持在浏览器中预览markdown文件

##### 安装插件
```
Plug iamcco/markdown-preview.vim
```

在`.vimrc`中加入如下配置
```
" markdown
let uname = system('uname -s')
if uname == "Darwin\n"
    let g:mkdp_path_to_chrome = "/Applications/Google\\ Chrome.app/Contents/MacOS/Google\\ Chrome"
else
    let g:mkdp_path_to_chrome = '/usr/bin/google-chrome-stable %U'
endif
nmap <silent> <F7> <Plug>MarkdownPreview
imap <silent> <F7> <Plug>MarkdownPreview
nmap <silent> <F8> <Plug>StopMarkdownPreview
imap <silent> <F8> <Plug>StopMarkdownPreview
```
