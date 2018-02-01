# vim + python 打造自己的IDE插件

> 参考：[vim+python打造自己的IDE插件推荐](http://blog.51cto.com/xujpxm/1909043)

> 参考：[把vim配置成顺手的python轻量级IDE](https://www.jianshu.com/p/f0513d18742a)

## 安装Vim插件管理器Vundle.vim

>  插件对比：
>> vim-pathogen VS Vundle.vim:
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

2. 下面贴出我的配置~/.vimrc
    - 基础配置部分

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

    - Vundle管理的插件：

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

    - NERDTree插件使用的配置信息：

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

3. 通过Vunder安装其他插件方法
  + 编辑~.vimrc，添加插件；启动vim，运行:PluginInstall
  + 或者：vim +PluginInstall +qall



