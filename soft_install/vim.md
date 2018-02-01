# vim + python 打造自己的IDE插件

> 参考：[vim+python打造自己的IDE插件推荐](http://blog.51cto.com/xujpxm/1909043)

> 参考：[把vim配置成顺手的python轻量级IDE](https://www.jianshu.com/p/f0513d18742a)

## 安装Vim插件管理器Vundle.vim

>  附插件对比：vim-pathogen VS Vundle.vim:
这两个插件都可谓是vim的神器，用来进行vim的插件管理。pathogen配置好之后使用方便之处在于只需要把你下载的vim插件放到~/.vim/bundle（也可自定义）目录下即可，而vundel每次需要更改vimrc文件，不过vundel的方便之处在于更改完vimrc文件之后，可以直接在vim里使用:PluginInstall来进行插件的一键安装，原理就是自动从GitHub等源上自动下载。
这里我选择的是vundle，因为可以一眼从配置文件看出我安装了哪些插件，不需要的插件直接注释掉即可。如下图Plugin部分就是我安装的插件，一目了然。

> git源：[Vunder.vim](https://github.com/VundleVim/Vundle.vim)

1. 安装
```
cd ~
mkdir -p ~/.vim/bundle
# 从github上得到项目的源码
git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim
``` 

2. 配置~/.vimrc
```
set nocompatible " be iMproved, required
filetype off " required
" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')
" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'
" The following are examples of different formats supported.
" Keep Plugin commands between vundle#begin/end.
" plugin on GitHub repo
Plugin 'tpope/vim-fugitive'
" plugin from http://vim-scripts.org/vim/scripts.html
" Plugin 'L9'
" Git plugin not hosted on GitHub
" Plugin 'git://git.wincent.com/command-t.git'
" git repos on your local machine (i.e. when working on your own plugin)
" Plugin 'file:///home/gmarik/path/to/plugin'
" The sparkup vim script is in a subdirectory of this repo called vim.
" Pass the path to set the runtimepath properly.
Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}
" Install L9 and avoid a Naming conflict if you've already installed a different version somewhere else.
Plugin 'ascenator/L9', {'name': 'newL9'}
" All of your Plugins must be added before the following line
call vundle#end() " required
filetype plugin indent on " required
" To ignore plugin indent changes, instead use:
"filetype plugin on
"
" Brief help
" :PluginList - lists configured plugins
" :PluginInstall - installs plugins; append '!' to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append '!' to refresh local cache
" :PluginClean - confirms removal of unused plugins; append '!' to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line
```

3. 通过Vunder安装其他插件方法

* 编辑~.vimrc，添加插件；启动vim，运行:PluginInstall
* 或者：vim +PluginInstall +qall



