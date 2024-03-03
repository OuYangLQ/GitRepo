# VimConfigTutor

## PREFACE
- 如果要重新配置 Vim，并且同时保存原来的 .vimrc 文件，您可以按照以下步骤进行操作：

1. 复制原始的 .vimrc 文件到另一个位置，例如您的主目录下或任何其他您选择的位置。假设您将其复制到主目录下并命名为 .vimrc.backup。
```
cp ~/.vimrc ~/.vimrc.backup
```
2. 打开您的 .vimrc 文件，删除或注释掉不需要的配置，并添加新的配置。
```
vim ~/.vimrc
```
3. 保存并退出 .vimrc 文件。

- 如果想要在配置 vim 过程中快速应用配置，可以将 R 键映射为 :source $MYVIMRC,命令 :source $MYVIMRC 用于重新加载当前用户的 Vim 配置文件。<br>
$MYVIMRC 是一个环境变量，指向当前用户的 Vim 配置文件，通常默认值为 ~/.vimrc（在 Unix 系统下）。<br>
因此，执行 :source $MYVIMRC 命令将重新加载并应用当前用户的 Vim 配置文件，使其中的更改生效。<br>
**注意：在使用下面的命令前需要先保存当前的配置**
```
map R :source $MYVIMRC<CR>
```

***

## map 
在 Vim 中，map 是用于创建键盘映射的命令之一。它用于定义一个递归的键盘映射，也就是说，它会解析已存在的映射。

map 命令的语法如下：
```
map {lhs} {rhs}
```

## noremap 
在 Vim 中，noremap 是一个用于创建键盘映射（Key Mapping）的命令。它用于定义一个不递归的键盘映射，也就是说，它会忽略已存在的映射。 

noremap 命令的语法如下：
```
noremap {lhs} {rhs}
```

## leader
在 Vim 中，leader 是一个特殊的键位，用于定义自定义键位映射的前缀。默认情况下，leader 键位是 \。
通过设置 mapleader 选项，您可以更改 leader 键位为您喜欢的任何其他键位。
```
let mapleader = "<Space>"
```
*请注意，leader 键的设置通常应该放在 .vimrc 配置文件中，并在 .vimrc 的开头设置，以确保在启动 Vim 时立即生效。*

***

## BasicConfiguration

- 光标定位到上次编辑的位置：
```
au BufReadPost * if line("''\"") > 1 && line("'\"") <= line("$") | exe "normal! g'\"" | endif
```

- 启用语法高亮:`syntax on`
- 禁用语法高亮:`syntax off`

- 将光标设置为块状：`set guicursor=a:block`<br>
- 启用行号：`set number`<br>
- 突出显示当前光标所在行：`set cursorline`<br>
- 启用文本自动换行：`set wrap`<br>
- 显示正在执行的命令（包括按键序列）的提示：`set showcmd`<br>
- 增强命令补全功能（使用方向键或 Tab 键进行切换）：`set wildmenu`、<br>
- 高亮搜索：`set hlsearch` 或者 `set incsearch`<br>
- 忽略大小写：`set ignorecase`<br>
- 智能地选择是否忽略大小写：`set smartcase`<br>
- 启用 list 选项以显示不可打印字符：`set list`
- 使用特殊符号显示 Tab 和空格：`set listchars=tab:▸\ ,trail:·`

## split-shortcut
- 向右分屏：`map sl :set splitright<CR>:vsplit<CR>`<br>
- 向左分屏：`map sh :set nosplitright<CR>:vsplit<CR>`<br>
- 向下分屏：`map sj :set splitbelow<CR>:split<CR>`<br>
- 向上分屏：`map sk :set nosplitbelow<CR>:split<CR>`<br>

- 光标向右`map <LEADER>l <C-w>l`
- 光标向左`map <LEADER>h <C-w>h`
- 光标向下`map <LEADER>j <C-w>j`
- 光标向上`map <LEADER>k <C-w>k`

***

## vim-plug
在linux环境下使用以下命令从 github 下载插件管理器：
```
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```
*如果终端出现这样的错误：<br>
curl: (7) Failed to connect to raw.githubusercontent.com port 443 after 27 ms: Connection refused<br>
可以进行以下尝试来修复错误：<br>
在终端输入：`ping raw.githubusercontent.com`<br>
如果终端显示：···localhost (127.0.0.1)··· 则可能是 DNS 解析错误<br>
在终端输入：`sudo vim /etc/resolv.conf` 来重新配置 DNS 服务<br>
现在提供两个配置选项：<br>
中国电信提供的免费 DNS Serve:`nameserve 114.114.114.114`<br>
Google 提供的免费 DNS Serve:`nameserve 8.8.8.8`*

## vim 插件推荐
1. 状态栏插件： `vim-airline/vim-airline`
2. 配色方案插件： `connorholyday/vim-snazzy`
3. 代码补全： `ycm-core/YouCompleteMe`<br>
*使用 vim-plug 进行插件安装时使用更安全的 SSH 协议，进行如下配置：<br>
`call plug#begin('~/.vim/plugged', { 'do': 'git clone --recursive' })`<br>
要配置子模块使用 SSH URL，你需要编辑项目的 .gitmodules 文件，并将子模块的 URL 配置从 HTTPS 改为 SSH：<br>
`url = git@github.com:username/repository.git`*

***

## ExpandConfiguration

### 查看全部配置选项：`:help option-list`

### 常用选项配置：

- 文本显示选项：<br>
number：显示行号。<br>
relativenumber：相对行号，显示当前行与光标所在行的相对行号。<br>
wrap：自动换行。<br>
cursorline：高亮当前行。<br>
showcmd：在底部显示正在输入的命令。<br>
hlsearch：高亮搜索结果。

- 编辑功能选项：<br>
autoindent：根据上一行自动缩进。<br>
tabstop：设置 Tab 键的宽度。<br>
expandtab：将 Tab 键转换为空格。<br>
shiftwidth：设置缩进宽度。<br>
smartindent：智能缩进。

- 文件类型相关选项：<br>
filetype plugin on：启用文件类型检测和相关插件。<br>
syntax on：启用语法高亮。

- 搜索和替换选项：<br>
ignorecase：忽略大小写进行搜索。<br>
smartcase：在搜索中自动切换大小写敏感/不敏感。<br>
incsearch：增量搜索，实时显示匹配结果。

- 其他选项：<br>
mouse：启用鼠标支持。<br>
encoding：设置文件编码。<br>
backup：生成备份文件。<br>
clipboard：设置剪贴板的操作方式。









