<!-- @format -->

# linux 系统常用软件工具

---

这些工具多数在 github 上都有开源实现,如果系统软件源中没有,可以从 github 上下载安装.
浏览器搜索关键字:`github ${工具名称}` 就可以找到相应的开源实现.

## 内置命令替代工具

### `exa`<--`ls`

(ls 的替代品)
exa 是一个用来显示文件和目录的命令行工具.

1. 安装

```shell
sudo apt install exa
```

### `htop`<--`top`

(top 的替代品)
htop 是一个用来显示系统进程的命令行工具.

1. 安装

```shell
sudo apt install htop
```

2. 使用

```shell
htop
```

### `btop`<--`top`

(top 的替代品)
btop 是一个用来显示系统资源的命令行工具.

1. 安装

```shell
sudo apt install btop
```

2. 使用

```shell
btop
```

### `zsh`<--`bash`

(bash 的替代品)
zsh 是一款强大的 shell 工具,它可以提供很多高级功能,比如自动补全,命令历史记录,自动纠错,自动跳转等.

1. 安装

```shell
sudo apt install zsh
```

2. 使用

查看可用的 shell

```shell
cat /etc/shells
```

设置 zsh 为默认 shell

```shell
chsh -s /bin/zsh
```

3. ohmyzsh

ohmyzsh 是一款基于 zsh 的插件管理工具,它可以安装很多有用的插件,比如 git, zsh-autosuggestions, zsh-syntax-highlighting 等.
github 地址:`https://github.com/ohmyzsh/ohmyzsh`

### `vim`<--`vi`

(vi 的替代品)
vim 是一个高级文本编辑器,它可以提供很多高级功能,并根据个人喜好进行定制.

1. 安装

```shell
sudo apt install vim
```

2. 使用

```shell
vim ${文件路径}
```

3. vimrc

该 vim 配置文件为 github 上的一位用户提供,已配置好常用功能,拥有最多的 Star.
github 地址:`https://github.com/amix/vimrc`

### `ripgrep`<--`grep`

(grep 的替代品)
ripgrep 是一个快速的搜索工具,它可以搜索文本文件,支持正则表达式.

1. 安装

```shell
sudo apt install ripgrep
```

2. 使用

```shell
rg ${搜索内容} ${文件路径}
```

### `bat`<--`cat`

(cat 的替代品)
bat 是一个用来显示文件内容的命令行工具,它可以高亮显示文件内容,并提供分页功能.

1. 安装

```shell
sudo apt install bat
```

2. 使用

请注意,可能由于与现有包发生冲突,您可能需要使用`batcat`命令才能使用 bat.

```shell
bat ${文件路径}
# 或
batcat ${文件路径}
```

### `fd`<--`find`

(find 的替代品)
fd 是一个用来搜索文件和目录的命令行工具,它可以支持正则表达式.

1. 安装

```shell
sudo apt install fd-find
```

2. 使用

请注意,可能由于与现有包发生冲突,您可能需要使用`fdfind`命令才能使用 fd.

```shell
fd ${搜索内容} ${指定路径}
# 或
fdfind ${搜索内容} ${指定路径}
```

## 常用工具

### neofetch

neofetch 是一个用来显示,系统信息的命令行工具.

1. 安装

```shell
sudo apt install neofetch
```

2. 使用

```shell
neofetch
```

### ncdu

ncdu 是一个用来显示磁盘使用情况的命令行工具.

1. 安装

```shell
sudo apt install ncdu
```

2. 使用

```shell
ncdu --color dark --exclude ${不包含的文件夹} ${需要分析的目录}
```

### tree

tree 是一个用来显示目录结构的命令行工具.

1. 安装

```shell
sudo apt install tree
```

2. 使用

```shell
tree
```

### 7zip

用于解压和压缩文件.

1. 安装

```shell
sudo apt install p7zip
```

2. 使用

```shell
# 解压
7za x filename.7z
# 压缩
7za a filename.7z dirname -o${输出目录}
# 显示压缩包内文件列表
7za l filename.7z
```

### telnet

telnet 用于远程登录服务器,可以用来测试网络连接及端口状况.

1. 安装

```shell
sudo apt install telnet
```

2. 使用

```shell
telnet ${host} ${端口}
```

### iotop

iotop 是一个用来显示磁盘 I/O 状态的命令行工具.

1. 安装

```shell
sudo apt install iotop
```

2. 使用

```shell
iotop
```

### atop

atop 是一个用来显示系统性能的命令行工具.

1. 安装

```shell
sudo apt install atop
```

2. 使用

```shell
atop
```

### glances

glances 是一个用来显示系统性能的命令行工具.

1. 安装

```shell
sudo apt install glances
```

2. 使用

```shell
glances
```

### ranger

Ranger 是一款基于文本的文件管理器,适用于 Linux 和 Unix 系统, 它通过终端界面提供直观的文件管理功能.

1. 安装

```shell
sudo apt install ranger
```

2. 使用

```shell
ranger
```
