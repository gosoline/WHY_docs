<!-- @format -->

# linux 下 ohmyzsh,miniconda 全局安装

linux 下为所有用户安装 omyzsh,miniconda 并配置全局环境变量

## 1. 安装 zsh

### 1.1 下载 zsh

ubuntu/debian 下安装 zsh

```shell
sudo apt update
sudo apt install zsh
```

centos/redhat 下安装 zsh

```shell
sudo yum update
sudo yum install zsh
```

### 1.2 设置 zsh 为默认 shell

```shell
# 查看当前可用shell列表
cat /etc/shells
# 更改root的默认shell
chsh -s /bin/zsh
```

## 2. 安装 ohmyzsh

### 2.1 下载 ohmyzsh

```shell
# 克隆ohmyzsh项目到`/opt/ohmyzsh`
git clone https://github.com/ohmyzsh/ohmyzsh.git /opt/ohmyzsh
# 根据模板创建一个基本的zsh配置
cp /opt/ohmyzsh/templates/zshrc.zsh-template /etc/zsh.d/ohmyzsh.zshrc
```

### 2.2 配置 ohmyzsh

创建配置文件`/etc/zsh.d/ohmyzsh.zshrc`,并添加:

```shell
# 添加环境变量
export ZSH=/opt/ohmyzsh  # 修改ohmyzsh安装目录
export ZSH_COMPDUMP=$HOME/.zcompdump  # 否则会[出现`rm: 无法删除 xxx`]
export XDG_CONFIG_HOME=$HOME/.config  # 否则会出现权限问题
export CONDARC=$HOME/.condarc  # 否则会出现权限问题

# 修改配置
ZSH_THEME="why_ys"  # 设置主题,主题样式文件在`/opt/ohmyzsh/themes`下,why_ys是我根据ys主题修改的,添加了python,conda环境信息等
plugins=(git zsh-syntax-highlighting zsh-autosuggestions)  # 启用插件,默认只有git,其它插件需自己添加
```

### 2.3 将 ohmyzsh 添加到 zsh 的全局配置

在`/etc/zshrc`或`/etc/zsh/zshrc`中:

```shell
# 在文件末尾添加
source /etc/zsh.d/ohmyzsh.zshrc
```

### 2.4 刷新 zsh 配置

```shell
source /etc/zshrc
```

## 3. 安装 miniconda

### 3.1 下载 miniconda

```shell
# 下载miniconda安装包
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
# 运行安装脚本,注意选择安装路径时安装到`/opt/miniconda3`
bash Miniconda3-latest-Linux-x86_64.sh
```

### 3.2 配置 miniconda

1. init conda 环境:

```shell
# 初始化conda环境
/opt/miniconda3/bin/conda init zsh
```

执行后会在`~/.zshrc`中添加 conda 环境初始化代码,并将 conda 命令添加到 PATH 中,如:

```shell
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/opt/miniconda3/bin/conda' 'shell.zsh' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/opt/miniconda3/etc/profile.d/conda.sh" ]; then
        . "/opt/miniconda3/etc/profile.d/conda.sh"
    else
        export PATH="/opt/miniconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

2. 修改为全局配置

创建配置文件`/etc/zsh.d/conda.zshrc`,并复制上一步生成的代码到里面:

### 3.3 将 miniconda 添加到 zsh 的全局配置

在`/etc/zshrc`或`/etc/zsh/zshrc`中:

```shell
# 在文件末尾添加
source /etc/zsh.d/conda.zshrc
```

> 注意:
> 如果 ohmyzsh 和 miniconda 都安装,在`/etc/zshrc`中,先 source ohmyzsh 的 zshrc,再 source conda 的 zshrc,否则会出现 PYTHON_VERSION 显示不正确

### 3.4 刷新 zsh 配置

```shell
source /etc/zshrc
```

# 附件

## 自定义 ohmyzsh 主题文件`why_ys.zsh-theme`

主要在 ys 主题的基础上添加了 conda 环境信息,python 版本信息,并修改了一些颜色和提示符样式.

```shell
# Clean, simple, compatible and meaningful.
# Tested on Linux, Unix and Windows under ANSI colors.
# It is recommended to use with a dark background.
# Colors: black, red, green, yellow, *blue, magenta, cyan, and white.
#
# Mar 2013 Yad Smood

# VCS
YS_VCS_PROMPT_PREFIX1=" %{$reset_color%}on%{$fg[blue]%} "
YS_VCS_PROMPT_PREFIX2=":%{$fg[cyan]%}"
YS_VCS_PROMPT_SUFFIX="%{$reset_color%}"
YS_VCS_PROMPT_DIRTY=" %{$fg[red]%}x"
YS_VCS_PROMPT_CLEAN=" %{$fg[green]%}o"

# Git info
local git_info='$(git_prompt_info)'
ZSH_THEME_GIT_PROMPT_PREFIX="${YS_VCS_PROMPT_PREFIX1}git${YS_VCS_PROMPT_PREFIX2}"
ZSH_THEME_GIT_PROMPT_SUFFIX="$YS_VCS_PROMPT_SUFFIX"
ZSH_THEME_GIT_PROMPT_DIRTY="$YS_VCS_PROMPT_DIRTY"
ZSH_THEME_GIT_PROMPT_CLEAN="$YS_VCS_PROMPT_CLEAN"

# SVN info
local svn_info='$(svn_prompt_info)'
ZSH_THEME_SVN_PROMPT_PREFIX="${YS_VCS_PROMPT_PREFIX1}svn${YS_VCS_PROMPT_PREFIX2}"
ZSH_THEME_SVN_PROMPT_SUFFIX="$YS_VCS_PROMPT_SUFFIX"
ZSH_THEME_SVN_PROMPT_DIRTY="$YS_VCS_PROMPT_DIRTY"
ZSH_THEME_SVN_PROMPT_CLEAN="$YS_VCS_PROMPT_CLEAN"

# HG info
local hg_info='$(ys_hg_prompt_info)'
ys_hg_prompt_info() {
    # make sure this is a hg dir
    if [ -d '.hg' ]; then
        echo -n "${YS_VCS_PROMPT_PREFIX1}hg${YS_VCS_PROMPT_PREFIX2}"
        echo -n $(hg branch 2>/dev/null)
        if [[ "$(hg config oh-my-zsh.hide-dirty 2>/dev/null)" != "1" ]]; then
            if [ -n "$(hg status 2>/dev/null)" ]; then
                echo -n "$YS_VCS_PROMPT_DIRTY"
            else
                echo -n "$YS_VCS_PROMPT_CLEAN"
            fi
        fi
        echo -n "$YS_VCS_PROMPT_SUFFIX"
    fi
}

# Conda info
local conda_info='$(conda_prompt_info)'
conda_prompt_info(){
    # 当前python路径
    export CURRENT_PYTHON_PATH=$(which python)
    # 检查当前python路径是否以$CONDA_PREFIX开头,$CONDA_PREFIX是conda安装路径
    if [ -n "$CONDA_DEFAULT_ENV" ]&&[[ $CURRENT_PYTHON_PATH == $CONDA_PREFIX* ]]; then
        echo -n "$CONDA_DEFAULT_ENV "
    else
        echo -n ""
    fi
}

# Python info
local python_info='$(python_prompt_info)'
python_prompt_info(){
    # 显示python版本号
    export PYTHON_VERSION=$(python --version 2>/dev/null | awk '{print $2}')
    if [ -n "$PYTHON_VERSION" ]; then
        echo -n "$PYTHON_VERSION"
    else
        echo -n ""
    fi
}

# Bracket info
local bracket_info='$(bracket_prompt_info)'
local left='${bracket_info: 1:1}'
local right='${bracket_info: -1}'
bracket_prompt_info(){
    if [[ -n "$CONDA_DEFAULT_ENV" || -n "$PYTHON_VERSION" ]]; then
        echo -n "()"
    else
        echo -n "%{$reset_color%}"
    fi
}


# Virtualenv
local venv_info='$(virtenv_prompt)'
YS_THEME_VIRTUALENV_PROMPT_PREFIX=" %{$fg[green]%}"
YS_THEME_VIRTUALENV_PROMPT_SUFFIX=" %{$reset_color%}%"
virtenv_prompt() {
    [[ -n "${VIRTUAL_ENV:-}" ]] || return
    echo "${YS_THEME_VIRTUALENV_PROMPT_PREFIX}${VIRTUAL_ENV:t}${YS_THEME_VIRTUALENV_PROMPT_SUFFIX}"
}

local exit_code="%(?,,C:%{$fg[red]%}%?%{$reset_color%})"

# Prompt format:
#
# PRIVILEGES USER @ MACHINE in DIRECTORY on git:BRANCH STATE [TIME] C:LAST_EXIT_CODE
# $ COMMAND
#
# For example:
#
# % ys @ ys-mbp in ~/.oh-my-zsh on git:master x [21:47:42] C:0
# $

PROMPT="
%{$fg[magenta]%}\
${left}\
${conda_info}\
${python_info}\
${right}\
%{$reset_color%}\
%{$terminfo[bold]$fg[blue]%}#%{$reset_color%} \
%(#,%{$bg[yellow]%}%{$fg[black]%}%n%{$reset_color%},%{$fg[cyan]%}%n) \
%{$reset_color%}@ \
%{$fg[green]%}%m \
%{$reset_color%}in \
%{$terminfo[bold]$fg[yellow]%}%~%{$reset_color%}\
${hg_info}\
${git_info}\
${svn_info}\
${venv_info}\
 \
[%*] $exit_code
%{$terminfo[bold]$fg[red]%}$ %{$reset_color%}"
```

## `ohmzsh.zshrc`文件示例

```shell
# If you come from bash you might have to change your $PATH.
# export PATH=$HOME/bin:$HOME/.local/bin:/usr/local/bin:$PATH

# Path to your Oh My Zsh installation.
# export ZSH="$HOME/.oh-my-zsh"
export ZSH="/opt/ohmyzsh"
export ZSH_COMPDUMP=$HOME/.zcompdump  # 否则会[出现`rm: 无法删除 xxx`]
export XDG_CONFIG_HOME=$HOME/.config  # 否则会出现权限问题
export CONDARC=$HOME/.condarc  # 否则会出现权限问题

# Set name of the theme to load --- if set to "random", it will
# load a random theme each time Oh My Zsh is loaded, in which case,
# to know which specific one was loaded, run: echo $RANDOM_THEME
# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
ZSH_THEME="why_ys"

# Set list of themes to pick from when loading at random
# Setting this variable when ZSH_THEME=random will cause zsh to load
# a theme from this variable instead of looking in $ZSH/themes/
# If set to an empty array, this variable will have no effect.
# ZSH_THEME_RANDOM_CANDIDATES=( "robbyrussell" "agnoster" )

# Uncomment the following line to use case-sensitive completion.
# CASE_SENSITIVE="true"

# Uncomment the following line to use hyphen-insensitive completion.
# Case-sensitive completion must be off. _ and - will be interchangeable.
# HYPHEN_INSENSITIVE="true"

# Uncomment one of the following lines to change the auto-update behavior
# zstyle ':omz:update' mode disabled  # disable automatic updates
# zstyle ':omz:update' mode auto      # update automatically without asking
# zstyle ':omz:update' mode reminder  # just remind me to update when it's time

# Uncomment the following line to change how often to auto-update (in days).
# zstyle ':omz:update' frequency 13

# Uncomment the following line if pasting URLs and other text is messed up.
# DISABLE_MAGIC_FUNCTIONS="true"

# Uncomment the following line to disable colors in ls.
# DISABLE_LS_COLORS="true"

# Uncomment the following line to disable auto-setting terminal title.
# DISABLE_AUTO_TITLE="true"

# Uncomment the following line to enable command auto-correction.
# ENABLE_CORRECTION="true"

# Uncomment the following line to display red dots whilst waiting for completion.
# You can also set it to another string to have that shown instead of the default red dots.
# e.g. COMPLETION_WAITING_DOTS="%F{yellow}waiting...%f"
# Caution: this setting can cause issues with multiline prompts in zsh < 5.7.1 (see #5765)
# COMPLETION_WAITING_DOTS="true"

# Uncomment the following line if you want to disable marking untracked files
# under VCS as dirty. This makes repository status check for large repositories
# much, much faster.
# DISABLE_UNTRACKED_FILES_DIRTY="true"

# Uncomment the following line if you want to change the command execution time
# stamp shown in the history command output.
# You can set one of the optional three formats:
# "mm/dd/yyyy"|"dd.mm.yyyy"|"yyyy-mm-dd"
# or set a custom format using the strftime function format specifications,
# see 'man strftime' for details.
# HIST_STAMPS="mm/dd/yyyy"

# Would you like to use another custom folder than $ZSH/custom?
# ZSH_CUSTOM=/path/to/new-custom-folder

# Which plugins would you like to load?
# Standard plugins can be found in $ZSH/plugins/
# Custom plugins may be added to $ZSH_CUSTOM/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
plugins=(git zsh-syntax-highlighting zsh-autosuggestions)

source $ZSH/oh-my-zsh.sh

# User configuration

# export MANPATH="/usr/local/man:$MANPATH"

# You may need to manually set your language environment
# export LANG=en_US.UTF-8

# Preferred editor for local and remote sessions
# if [[ -n $SSH_CONNECTION ]]; then
#   export EDITOR='vim'
# else
#   export EDITOR='nvim'
# fi

# Compilation flags
# export ARCHFLAGS="-arch $(uname -m)"

# Set personal aliases, overriding those provided by Oh My Zsh libs,
# plugins, and themes. Aliases can be placed here, though Oh My Zsh
# users are encouraged to define aliases within a top-level file in
# the $ZSH_CUSTOM folder, with .zsh extension. Examples:
# - $ZSH_CUSTOM/aliases.zsh
# - $ZSH_CUSTOM/macos.zsh
# For a full list of active aliases, run `alias`.
#
# Example aliases
# alias zshconfig="mate ~/.zshrc"
# alias ohmyzsh="mate ~/.oh-my-zsh"
```
