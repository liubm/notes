## vim 插件管理
```
yum install git -y
git clone https://github.com/gmarik/vundle.git  ~/.vim/bundle/vundle
```
## vim配置文件
```
"##############################################################
" basic config
"##############################################################
set nocompatible "关闭vim一致性原则,避免和以前版本的一些bug和局限
set number "显示行号
set backspace=indent,eol,start
set ruler "设置在编辑过程中右下角显示光标的行列信息
set showcmd "在状态栏显示正在输入的命令
filetype on "检测文件类型
filetype indent on "针对不同文件采用不同的缩进方式
filetype plugin indent on
"set background=dark "背景使用黑色
"syntax enable "语法高亮显示
"syntax on
"格式对齐
set autoindent       "自动对齐
set smartindent      "根据上文对齐格式自动对齐
"set cindent         "C语言格式对齐
set expandtab "将tab键自动转换为空格
set tabstop=4 "设置tab键长度
set shiftwidth=4     "设置自动对齐4个空格

"filetype plugin indent on "启用智能补全
set smarttab "设置退格键可以删除4个空格
set softtabstop=4
set showmatch "设置比配模式, 类似{ 和 } 匹配
"set t_Co=256 "指定配色方案为256色
"设置编码方式
set encoding=utf-8
set fileencodings=utf-8,big5,gb2312,gb18030,ucs-bom,cp936,euc-jp,euc-kr,latin1 "自动判断编码时  依次尝试一下编码
set history=1000 "历史记录条数
set guioptions-=T "去除GUI版本中的toolbar
filetype plugin on "允许插件
"set mouse=a "设置在vim中可以使用鼠标
"set backspace=indent,eol,start "设置backspace的工作方式
"set nobackup "取消备份  禁止生成临时文件
"set noswapfile
set vb t_vb= "当vim进行编辑时,如果命令错误,会发出一个响声,该设置取消响声
set ignorecase "设置搜索时忽略大小写
set incsearch "在搜索时自动向后查找


"##############################################################
" plugin config
"##############################################################
"
set rtp+=~/.vim/bundle/vundle/

call vundle#rc()

" 设置NerdTree
map <F3> :NERDTreeMirror<CR>
map <F3> :NERDTreeToggle<CR>
nnoremap <C-l> gt
nnoremap <C-h> gT
"original repos on github
Bundle 'vim-scripts/The-NERD-tree'
"Bundle 'tpope/vim-fugitive'
"Bundle 'Lokaltog/vim-easymotion'
"Bundle 'rstacruz/sparkup', {'rtp': 'vim/'}
"Bundle 'tpope/vim-rails.git'
"Bundle 'scrooloose/nerdtree'
"Bundle 'kien/ctrlp.vim'
"Bundle 'msanders/snipmate.vim'
"Bundle 'mileszs/ack.vim'
"Bundle 'Shougo/neocomplcache.vim'
"Bundle 'Townk/vim-autoclose'
"Bundle 'Lokaltog/vim-easymotion'
"Bundle 'Lokaltog/vim-powerline'

" plugin address
" https://github.com/vim-scripts
" example:
" :BundleInstall 
" let Vundle manage Vundle  
" " required!  
" Bundle 'gmarik/vundle'  
"   
"   " My Bundles here:  /* 插件配置格式 */  
"   "    
"   " original repos on github
"   （Github网站上非vim-scripts仓库的插件，按下面格式填写）  
"   Bundle 'tpope/vim-fugitive'  
"   Bundle 'Lokaltog/vim-easymotion'  
"   Bundle 'rstacruz/sparkup', {'rtp': 'vim/'}  
"   Bundle 'tpope/vim-rails.git'  
"   " vim-scripts repos  （vim-scripts仓库里的，按下面格式填写）  
"   Bundle 'L9'  
"   Bundle 'FuzzyFinder'  
"   " non github repos  (非上面两种情况的，按下面格式填写)  
"   Bundle 'git://git.wincent.com/command-t.git'  
"   " ...  
"     
"     filetype plugin indent on    " required!  /** vimrc文件配置结束 **/  
"     "                                          /** vundle命令 **/  
"     " Brief help  
"     " :BundleList          - list configured bundles  
"     " :BundleInstall(!)    - install(update) bundles  
"     " :BundleSearch(!) foo - search(or refresh cache first) for foo 
"
"     " :BundleClean(!)      - confirm(or auto-approve) removal of unused
"     bundles  
"     "    
"     " see :h vundle for more details or wiki for FAQ  
"     " NOTE: comments after Bundle command are not allowed.. 
"YouCompleteMe —— 代码补全
"Syntastic —— 语法检查
"SuperTab —— 使 Tab 快捷键具有更快捷的上下文提示功能
"Ctags —— 实现变量名、函数名的跳转（需遍历源代码文件生成 tags 文件）
"Cscope —— 升级版 Ctags
"TagList —— 显示当前文件中的宏、全局变量、函数等 tag（类似于 SourceInsight 的功能）
"Tagbar —— TagList 的替代品（更适合于 C++）
"AutoPairs —— 自动插入和格式化括号
"Powerline —— 状态栏
"Vim-airline —— Powerline 的替代品
"Echofunc —— 自动显示函数声明
"Snipmate —— 自动插入代码（代码重用工具）
"NERDTree —— 文件浏览器（树形目录）
"Ctrlp —— 文件浏览器（重新定义打开目录和文件的方式，更适用于大规模项目文件的浏览）
"MiniBufferExplorer —— 缓冲区文件管理器
"NERDCommenter —— 快速注释
"Undotree —— 支持 undo 和 redo
"Gdbmgr —— 调试器
"Molokai —— 颜色主题
```