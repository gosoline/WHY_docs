<!-- @format -->

# vscode 远程 linux(包括离线`vscode-server`安装,免密登录方法)

本教程前提是安装并配置好 ssh 服务

## 1. vscode 安装安装远程所需扩展及配置

## 1.1 安装扩展

在`vscode` 扩展中搜索`Remote - SSH`,下载安装

## 1.2 通过 ssh 远程连接

### 1.2.1 通过 ssh 连接命令连接

在`vscode` 中依次点击 `远程资源管理器->新建远程`,在打开的连接命令窗口中输入命令

```shell
ssh <user>@<hostname>:[port]
```

-   user: 是在远程服务器上的用户名
-   hostname: 远程服务器的主机名或 IP 地址
-   port: SSH 连接的端口号(默认为 22)

输入后按`Enter`键选择要更新的配置文件,一般选择第一个也就是`C:\Users\${你的用户名}\.ssh\config`

### 1.2.2 通过更新 ssh 配置文件连接

在`vscode` 中依次点击`远程资源管理器->打开SSH配置文件`选择要更新的 SSH 配置文件,一般选择第一个也就是`C:\Users\${user}\.ssh\config`,打开后编辑配置并保存:

```
Host xxx
  HostName xxx.xxx.xxx.xxx
  Port xx
  User xxx
  IdentityFile "xxx"
```

-   Host:这是一个主机别名,你可以使用这个别名来代替实际的主机名进行连接.
-   HostName:这是指定远程主机的 IP 地址或主机名.
-   Port:这是指定 SSH 连接的端口号.
-   User:这是指定用于连接远程主机的用户名.
-   IdentityFile:这是指定用于身份验证的私钥文件的路径.(免密登录才需要,请看[3. 免密登录](#3-免密登录))

_如果要配置多个远程,继续在此文件追加配置即可_

**1.2.1 或 1.2.2 完成后点击`远程资源管理器`的`刷新`,此时`远程资源管理器`会出现刚配置的远程连接,根据需要选择`在当前窗口连接`或`在新窗口中连接`,此时会让你输入密码,然后会在远程端下载所需文件(需要联网),如果无法联网,请看[2. 离线下载 vscode-server 并安装](#2-离线下载vscode-server并安装)**

## 2. 离线下载`vscode-server`并安装

如果远程端不能联网可以下载包离线安装,下载 vscode-server 的 url 需要和 vscode 客户端版本的 commit-id 对应.通过 vscode 面板的`帮助->关于`可以获取该信息,复制信息,我当前版本如下(_提交后面对应的就是 commit_id_):

```
版本: 1.89.1 (system setup)
提交: dc96b837cf6bb4af9cd736aa3af08cf8279f7685
日期: 2024-05-07T05:13:33.891Z
Electron: 28.2.8
ElectronBuildId: 27744544
Chromium: 120.0.6099.291
Node.js: 18.18.2
V8: 12.0.267.19-electron.0
OS: Windows_NT x64 10.0.19044
```

### 2.1 旧版离线包下载

vscode-server 下载地址如下,其中 commit_id 是上面复制的提交 id:

```
x86:
https://update.code.visualstudio.com/commit:${commit_id}/server-linux-x64/stable
arm:
https://update.code.visualstudio.com/commit:${commit_id}/server-linux-arm64/stable
```

将下载的文件 `vscode-server-linux-x64.tar.gz` 解压解包后名为 `vscode-server-linux-x64` 文件夹改名为 `${commit_id}` 放在 `/home/${user}/.vscode-server/bin/` 目录下.

### 2.2 新版离线包下载

在某次更新后远程端的 .vscode-server 目录结构发生变化:

```
📦.vscode-server
 ┣━ 📁bin  # 存放旧方法下的vscode commit相关文件
 ┃   ┗━ 📁${commit_id1}
 ┃   ┗━ 📁${commit_id2}
 ┃   ┗━ ···
 ┣━ 📁cli  # 存放新方法下的vscode commit相关文件
 ┃   ┗━ 📁servers
 ┃   ┃   ┗━ 📁Stable-${commit_id}
 ┃   ┃   ┃   ┗━ 📁servers
 ┃   ┃   ┃   ┗━ ···
 ┃   ┃   ┗━ ···
 ┃   ┗━ 📜iru.json  # 存放最近的vscode commit_id
 ┣━ 📜code-${commit_id}  # 存放vscode_cli_alpine_x64_cli.tar.gz解压后名为code的文件,并将其改名为code-${commit_id}
 ┣━ 📁data
 ┗━ 📁extensions
```

现在需要安装两个文件,两个文件的下载地址如下:

```
x86:
https://vscode.download.prss.microsoft.com/dbazure/download/stable/${commit_id}/vscode-server-linux-x64.tar.gz
https://vscode.download.prss.microsoft.com/dbazure/download/stable/${commit_id}/vscode_cli_alpine_x64_cli.tar.gz

arm:
https://vscode.download.prss.microsoft.com/dbazure/download/stable/${commit_id}/vscode-server-linux-arm64.tar.gz
https://vscode.download.prss.microsoft.com/dbazure/download/stable/${commit_id}/vscode_cli_alpine_arm64_cli.tar.gz
```

第一个文件 `vscode-server-linux-x64.tar.gz` 解压解包后名为 `vscode-server-linux-x64` 文件夹改名为 `server` 放在 `/home/${user}/.vscode-server/cli/servers/Stable-${commit_id}/` 目录下.

第二个文件 `vscode_cli_alpine_x64_cli.tar.gz` 解压解包后名为 `code` 的文件改名为 `code-${commit_id}`放在`/home/${user}/.vscode-server/`目录下

### 2.3 无法连接可能问题

如果仍然连接不上,则可能需要修改`.vscode-server`文件夹及其子目录的权限,例如权限改为`700`,再尝试连接:

```shell
chmod -R 700 /home/${user}/.vscode-server/
```

## 3. 免密登录

### 3.1 生成 SSH 密钥

生成 ssh 使用的公钥/密钥对,请从客户端上的 PowerShell 或 cmd 提示符运行以下命令,具体使用方法详细见:[微软官方](https://learn.microsoft.com/zh-cn/windows-server/administration/openssh/openssh_keymanagement#user-key-generation)

```shell
ssh-keygen -t rsa
```

输入命令执行完成后会生成`C:\Users\${user}\.ssh`,里面会有 `id_rsa`(私钥),
`id_rsa.pub`(公钥)两个文件,这两个是默认名称,在执行命令时可以添加选项选择不同文件名,如果更改文件名,后面步骤对应文件路径也要更改

### 3.2 添加公钥到远程服务器

`id_rsa.pub`(公钥)生成后,打开复制内容,打开远程主机`/home/${user}/.ssh/authorized_keys`文件,如果文件不存在就创建,然后粘贴复制的公钥内容,然后打开[1.2.2 通过更新 ssh 配置文件连接](#122-通过更新-ssh-配置文件连接)中的`C:\Users\${user}\.ssh\config`配置文件,在你要连接的`Host`下配置`IdentityFile`,后面填写`id_rsa`(私钥)路径,并保存:

```
Host xxx
  HostName xxx.xxx.xxx.xxx
  Port xx
  User xxx
  IdentityFile "C:\Users\${user}\.ssh\id_rsa"
```

如果手动创建 /home/${user}/.ssh/authorized_keys,需要更改其权限:

```shell
chmod 700 /home/${user}/.ssh
chmod 600 /home/${user}/.ssh/authorized_keys
```

### 3.3 验证方式

3.2 完成后点击`vscode`中`远程资源管理器`的`刷新`,此时`远程资源管理器`会出现刚配置的远程连接,根据需要选择`在当前窗口连接`或`在新窗口中连接`,点击后确认左下角进入到连接成功的状态,期间没有提示输入密码的窗口,即代表成功了
