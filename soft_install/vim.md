# vim + python 打造自己的IDE插件

> 参考：[vim+python打造自己的IDE插件推荐](http://blog.51cto.com/xujpxm/1909043)

> 参考：[把vim配置成顺手的python轻量级IDE](https://www.jianshu.com/p/f0513d18742a)

## 插件对比
+ vim插件管理器

> vim-pathogen VS Vundle.vim
> 这两个插件都可谓是vim的神器，用来进行vim的插件管理。pathogen配置好之后使用方便之处在于只需要把你下载的vim插件放到~/.vim/bundle（也可自定义）目录下即可，而vundel每次需要更改vimrc文件，不过vundel的方便之处在于更改完vimrc文件之后，可以直接在vim里使用:PluginInstall来进行插件的一键安装，原理就是自动从GitHub等源上自动下载。
> 这里我选择的是vundle，因为可以一眼从配置文件看出我安装了哪些插件，不需要的插件直接注释掉即可

+ python支持

> Jedi-vim  VS  Python-mode  VS  YouCompleteMe
> python-mode:
>    优点：能够自动补全，自带python语法检测和代码折叠等功能，很强大。
>    缺点：自动补全时顺带显示函数的帮助信息，页面显示不够简洁、美观；语法检测功能一般。
> YouCompleteMe：
>    优点：自动补全，界面简洁，支持多语言，功能非常强大、完整。三者之中在github上star数量最多。
>    缺点：可能由于功能过于强大,加语法检测之后加载相对稍慢。配置略繁琐。
> jedi-vim：
>    优点：优点对我来说，就是上面两个的缺点它都弥补了。加载速度挺快，页面也挺简洁。
>    缺点：没有语法检测；功能没YCM强大，但是够用足矣。

+ python语法检测

> 有了自动补全之后就是语法检测，个人倾向pep8标准，而且希望语法错误修正之后能够被编辑器马上识别。
> 我测过用以下几种做checker：
> flake8、pep257、pep8、pycodestyle、syntastic、pydocstyle、pyflakes、pylama、pylint、python
> 而最终我选择了用插件："w0rp/ale",它的语法检测最全面，界面简洁，错误修正之后能够被马上识别出，而且是异步的，不必担心加载过慢崩溃等问题。

+ 加强版自动补全

> 之前提到在vim里面python的自动补全，为了使vim的功能更加强大，介绍一款插件neocomplete.vim，使用它可谓让vim的补全无处不在。

+ 目录树插件

> 目录树插件自然是NERDTree，外加一个vim-nerdtree-tabs补强功能。

## 安装Vundle [git源Vunder.vim](https://github.com/VundleVim/Vundle.vim)

```
cd ~
mkdir -p ~/.vim/bundle
# 从github上得到项目的源码
git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim
``` 
> 通过Vunder安装其他插件方法:
> + 编辑~.vimrc，添加插件；启动vim，运行:PluginInstall
> + 或者：vim +PluginInstall +qall

## 配置~/.vimrc

1. 基础配置部分
```
" 显示行号
set nu
" 去掉vi的一致性（不要使用vi的键盘模式，而是vim自己的）
set nocompatible
" 隐藏滚动条
set guioptions-=r 
set guioptions-=L
set guioptions-=b
" 隐藏顶部标签栏
set showtabline=0
" 设置字体
set guifont=Monaco:h13
" 开启语法高亮
syntax on
" 使回格键（backspace）正常处理indent, eol, start等
"set backspace=index,eol,start
" 设置背景色
set background=dark
" 设置table长度
set tabstop=4
set shiftwidth=4
" 显示匹配的括号
set showmatch
" 距离顶部和底部5行
set scrolloff=5
" 命令行为两行
set laststatus=2
" 设定默认编码
set fenc=utf-8
" 启用鼠标
"set mouse=a
"set selection=exclusive
"set selectmode=mouse,key
"set matchtime=5
" 检索时忽略大小写忽略大小写
"set ignorecase
" 允许backspace和光标键跨越行边界
"set whichwrap+=<,>,h,l
" 文件在Vim之外修改过，自动重新读入
"set autoread
" 突出显示当前行
set cursorline
" 突出显示当前列
set cursorcolumn
set ts=4
set tabstop=4 "设置table长度"
set expandtab "用空格代替制表符"
set softtabstop=4 "一缩进为4"
set shiftwidth=4
set smartindent "智能缩进"
set cindent "C语言风格缩进"
set autoindent "自动缩进"
" 启用语法高亮度
syntax enable
```

2. Vundle管理的插件：
```
" 使用Vundle管理其他插件
" Vundle config plugin start
filetype off " required
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
Plugin 'VundleVim/Vundle.vim'
" python 自动补全 Jedi-vim 
Plugin 'davidhalter/jedi-vim'
" python 语法检测 pep8
Plugin 'w0rp/ale'
" python 加强版自动补全 neocomplete.vim
Plugin 'Shougo/neocomplete.vim'
" NERDTree 
Plugin 'scrooloose/nerdtree'
" NERDTree增强功能 vim-nerdtree-tabs
Plugin 'jistr/vim-nerdtree-tabs'
" nerdtree-git-plugin
Plugin 'Xuyuanp/nerdtree-git-plugin'
" Plugin 'tpope/vim-fugitive'
" Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}
" Plugin 'ascenator/L9', {'name': 'newL9'}
call vundle#end()
filetype plugin indent on
" Vundle config plugin end
" Brief help
" :PluginList - lists configured plugins
" :PluginInstall - installs plugins; append '!' to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append '!' to refresh local cache
" :PluginClean - confirms removal of unused plugins; append '!' to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line
```

3. NERDTree插件使用的配置信息：
```
" 打开或关闭NERDTree快捷键
map <F2> :NERDTreeToggle<CR>
" 显示行号
let NERDTreeShowLineNumbers=1
let NERDTreeAutoCenter=1
" 是否显示隐藏文件
let NERDTreeShowHidden=1
" 设置宽度
let NERDTreeWinSize=31
" 在终端启动vim时，共享NERDTree
let g:nerdtree_tabs_open_on_console_startup=1
" 忽略以下文件的显示
let NERDTreeIgnore=['\.pyc','\~$','\.swp']
" 显示书签列表
let NERDTreeShowBookmarks=1
" 启动vim自动打开NERDTree
" autocmd VimEnter * NERDTree
" 打开新的buffer时自动定位到编辑窗口 
" autocmd VimEnter * wincmd p
" git信息直接在NERDTree中显示出来
let g:NERDTreeIndicatorMapCustom = {
    \ "Modified"  : "✹",
    \ "Staged"    : "✚",
    \ "Untracked" : "✭",
    \ "Renamed"   : "➜",
    \ "Unmerged"  : "═",
    \ "Deleted"   : "✖",
    \ "Dirty"     : "✗",
    \ "Clean"     : "✔︎",
    \ "Unknown"   : "?"
    \ }
```

