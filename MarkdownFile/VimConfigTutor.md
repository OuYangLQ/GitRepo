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

- 如果想要在配置 vim 过程中快速应用配置，可以将 R 键映射为 :source $MYVIMRC,命令 :source $MYVIMRC 用于重新加载当前用户的 Vim 配置文件。$MYVIMRC 是一个环境变量，指向当前用户的 Vim 配置文件，通常默认值为 ~/.vimrc（在 Unix 系统下）。因此，执行 :source $MYVIMRC 命令将重新加载并应用当前用户的 Vim 配置文件，使其中的更改生效。<br>
**注意：在使用下面的命令前需要先保存当前的配置**
```
map R :source $MYVIMRC<CR>
```
## syntaxhighlighting
- 启用语法高亮:`syntax on`
- 禁用语法高亮:`syntax off`

## guicursor
将光标设置为块状：`set guicursor=a:block`

## number
启用行号：`set number`

## cursorline
突出显示当前光标所在行：`set cursorline`

## wrap
启用文本自动换行：`set wrap`

## showcmd
显示正在执行的命令（包括按键序列）的提示：`set showcmd`

## wildmenu
增强命令补全功能（使用方向键或 Tab 键进行切换）：`set wildmenu`、

## hlsearch
高亮搜索：`set hlsearch` 或者 `set incsearch`

## ignorecase
忽略大小写：`set ignorecase`

## smartcase
智能地选择是否忽略大小写：`set smartcase`

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

