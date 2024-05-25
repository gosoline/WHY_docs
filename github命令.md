<!-- @format -->

这是 Git 的使用说明,它列出了常见的 Git 命令,以及它们在不同情况下的用法.

1. 开始一个工作区（参见:git help tutorial）

    - clone:将存储库克隆到一个新目录中
    - init:创建一个空的 Git 存储库或重新初始化一个现有的存储库

2. 处理当前的更改（参见:git help everyday）

    - add:将文件内容添加到索引中
    - mv:移动或重命名文件、目录或符号链接
    - restore:恢复工作树中的文件
    - rm:从工作树和索引中删除文件

3. 检查历史和状态（参见:git help revisions）

    - bisect:使用二分查找找到引入错误的提交
    - diff:显示提交之间、提交和工作树之间等的更改
    - grep:打印与模式匹配的行
    - log:显示提交日志
    - show:显示各种类型的对象
    - status:显示工作树状态

4. 扩展、标记和调整你的公共历史

    - branch:列出、创建或删除分支
    - commit:记录对存储库的更改
    - merge:将两个或多个开发历史记录合并在一起
    - rebase:在另一个基准点之上重新应用提交
    - reset:将当前的 HEAD 重置为指定的状态
    - switch:切换分支
    - tag:创建、列出、删除或验证使用 GPG 签名的标签对象

5. 协作（参见:git help workflows）
    - fetch:从另一个存储库下载对象和引用
    - pull:从另一个存储库或本地分支获取并集成
    - push:更新远程引用以及关联的对象

使用'git help -a'和'git help -g'列出可用的子命令和一些概念指南.使用'git help <command>'或'git help <concept>'阅读有关特定子命令或概念的说明.使用'git help git'获取系统的概述.

```shell
#这个命令用于设置全局的用户邮箱,将邮箱地址替换成您自己的邮箱地址.
git config --global user.email "2538796265@qq.com"
# 这个命令用于设置全局的用户名,将用户名替换成您自己的用户名.
git config --global user.name "why"
# 这个命令用于生成SSH密钥对,其中的邮箱地址应该与前面设置的邮箱地址一致.生成的密钥对将用于与远程Git仓库进行安全的通信.
ssh-keygen -t rsa -C "2538796265@qq.com"
# 在当前目录中创建一个新的 Git 仓库
git init
```

```bash
# 这个命令用于将远程Git仓库的地址添加到本地仓库,并将其命名为"origin".将地址替换成您自己的远程仓库地址.
git remote add origin git@github.com:gosoline/dpfwt.git
# 这个命令与前一个命令类似,只是使用HTTPS协议而不是SSH协议来与远程仓库进行通信.
git remote add origin https://github.com/gosoline/dpfwt.git
# 这个命令用于查看当前仓库已经配置的远程仓库地址.
git remote -v
# 移除与该别名相关联的远程仓库链接,"origin" 是一个远程仓库的别名
git remote remove origin
# 将代码提交至暂存区(git add . 默认将所有文件提交至本地仓库)
git add .
# 将暂存区中的更改提交到本地仓库,并附带一个简短的提交说明备注.
git commit -m "提交说明备注"
# 这个命令用于在使用HTTPS协议与远程仓库通信时禁用SSL证书验证.在某些情况下,可能需要禁用证书验证才能正常连接到远程仓库.请注意,这是一个不安全的操作,只应在特定情况下使用.
git config --global http.sslVerify false
# 这个命令用于将本地仓库的代码推送到远程仓库.其中的"origin"是之前添加的远程仓库名字,"main"是要推送的本地分支名字.根据您的需要,可以将"main"替换成其他分支名字.
git push -u origin main
```
