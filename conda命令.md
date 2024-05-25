<!-- @format -->

conda 相关命令

可以使用`conda xxx -h`(`例如 conda clean -h`)查看各个命令的使用方法

下面是`conda -h`的翻译内容

```
conda是一个用于管理和部署应用程序、环境和软件包的工具.

选项:
  -h, --help          显示帮助信息并退出.
  -v, --verbose       可以多次使用.一次用于详细输出,两次用于INFO日志,三次用于DEBUG日志,四次用于TRACE日志.
  --no-plugins        禁用所有不内置在conda中的插件.
  -V, --version       显示conda版本号并退出.

命令:
  可用以下内置和插件子命令.

  COMMAND
    clean               删除未使用的软件包和缓存.
    compare             比较conda环境之间的软件包.
    config              修改.condarc中的配置值.
    content-trust       Conda的签名和验证工具
    create              从指定的软件包列表创建一个新的conda环境.
    doctor              显示环境的健康报告.
    env                 查看`conda env --help`.
    info                显示有关当前conda安装的信息.
    init                初始化与shell的交互.
    install             将一系列软件包安装到指定的conda环境中.
    list                列出conda环境中已安装的软件包.
    notices             检索最新的通道通知.
    package             创建低级conda软件包.（实验性功能）
    remove (uninstall)  从指定的conda环境中删除一系列软件包.
    rename              重命名现有环境.
    repoquery           高级搜索repodata.
    run                 在conda环境中运行可执行文件.
    search              使用MatchSpec格式搜索软件包并显示相关信息.
    update (upgrade)    将conda软件包更新到最新兼容版本.
```
