<!-- @format -->

# linux 系统常用软件工具

## 1. neofetch

neofetch 是一个用来显示,系统信息的命令行工具.

1. 安装

```shell
sudo dnf install neofetch
```

2. 使用

```shell
neofetch
```

## 2. tree

tree 是一个用来显示目录结构的命令行工具.

1. 安装

```shell
sudo dnf install tree
```

2. 使用

```shell
tree
```

## 3. htop

htop 是一个用来显示系统进程的命令行工具,是 top 命令的增强版.

1. 安装

```shell
sudo dnf install htop
```

2. 使用

```shell
htop
```

## 3. zsh

zsh 是一款强大的 shell 工具,它可以提供很多高级功能,比如自动补全,命令历史记录,自动纠错,自动跳转等.

1. 安装

```shell
sudo dnf install zsh
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

## 4. 7zip

用于解压和压缩文件.

1. 安装

```shell
sudo dnf install p7zip
```

2. 使用

```shell
# 解压
7za x filename.7z
# 压缩
7za a filename.7z dirname
# 显示压缩包内文件列表
7za l filename.7z
```
