<!-- @format -->

# python 脚本打包成可执行文件: pyinstaller

## 1. 下载 pyinstaller

在终端输入下载命令

```shell{.line-numbers}
pip install pyinstaller
```

## 2. 命令行打包

在终端进入当前工作目录,输入命令

```shell{.line-numbers}
pyinstaller -D -w --add-data 'resources:resources' --add-data 'bin:bin' -i '风机.ico' -n 'dpfwt' 'main.py'
```

### 2.1 pyinstaller 参数表

| 参数                                                                  | 描述                                                              |
| --------------------------------------------------------------------- | ----------------------------------------------------------------- |
| `-h                                                                 ` | 显示帮助信息.                                                     |
| `-v                                                                 ` | 显示详细的输出信息.                                               |
| `-D                                                                 ` | 生成一个目录,包含可执行文件和所有依赖的文件.                      |
| `-F                                                                 ` | 生成一个单个的可执行文件.                                         |
| `--specpath DIR                                                     ` | 指定生成的.spec 文件的存储路径.                                   |
| `-n NAME                                                            ` | 指定生成的可执行文件的名称.                                       |
| `--contents-directory CONTENTS_DIRECTORY                            ` | 指定生成的目录结构的根目录.                                       |
| `--add-data SOURCE:DEST                                             ` | 将文件或目录添加到可执行文件中.                                   |
| `--add-binary SOURCE:DEST                                           ` | 将二进制文件添加到可执行文件中.                                   |
| `-p DIR                                                             ` | 添加额外的模块搜索路径.                                           |
| `--hidden-import MODULENAME                                         ` | 将指定的模块作为隐藏导入进行处理.                                 |
| `--collect-submodules MODULENAME                                    ` | 将指定模块及其所有子模块收集到可执行文件中.                       |
| `--collect-data MODULENAME                                          ` | 将指定模块及其所有数据文件收集到可执行文件中.                     |
| `--collect-binaries MODULENAME                                      ` | 将指定模块及其所有二进制文件收集到可执行文件中.                   |
| `--collect-all MODULENAME                                           ` | 将指定模块及其所有子模块、数据文件和二进制文件收集到可执行文件中. |
| `--copy-metadata PACKAGENAME                                        ` | 将指定包的元数据复制到可执行文件中.                               |
| `--recursive-copy-metadata PACKAGENAME                              ` | 递归复制指定包及其所有依赖的元数据到可执行文件中.                 |
| `--additional-hooks-dir HOOKSPATH                                   ` | 添加额外的钩子目录.                                               |
| `--runtime-hook RUNTIME_HOOKS                                       ` | 指定运行时钩子文件.                                               |
| `--exclude-module EXCLUDES                                          ` | 排除指定的模块.                                                   |
| `--splash IMAGE_FILE                                                ` | 指定启动画面的图像文件.                                           |
| `-d {all,imports,bootloader,noarchive}                              ` | 指定调试级别.                                                     |
| `--python-option PYTHON_OPTION                                      ` | 传递给 Python 解释器的选项.                                       |
| `-s                                                                 ` | 生成一个控制台程序而不是一个窗口程序.                             |
| `--noupx                                                            ` | 禁用 UPX 压缩.                                                    |
| `--upx-exclude FILE                                                 ` | 指定不压缩的文件.                                                 |
| `-c                                                                 ` | 生成一个控制台程序.                                               |
| `-w                                                                 ` | 生成一个窗口程序.                                                 |
| `--hide-console {minimize-late,hide-late,minimize-early,hide-early} ` | 控制控制台窗口的显示方式.                                         |
| `-i <FILE.ico or FILE.exe,ID or FILE.icns or Image or "NONE">       ` | 指定可执行文件的图标.                                             |
| `--disable-windowed-traceback                                       ` | 禁用窗口程序的回溯功能.                                           |
| `--version-file FILE                                                ` | 指定可执行文件的版本信息.                                         |
| `-m <FILE or XML>                                                   ` | 指定可执行文件的元数据.                                           |
| `-r RESOURCE                                                        ` | 将资源文件添加到可执行文件中.                                     |
| `--uac-admin                                                        ` | 请求管理员权限.                                                   |
| `--uac-uiaccess                                                     ` | 请求 UI 访问权限.                                                 |
| `--argv-emulation                                                   ` | 启用命令行参数仿真.                                               |
| `--osx-bundle-identifier BUNDLE_IDENTIFIER                          ` | 指定生成的 OS X 应用程序的 Bundle Identifier.                     |
| `--target-architecture ARCH                                         ` | 指定目标架构.                                                     |
| `--codesign-identity IDENTITY                                       ` | 指定代码签名的标识.                                               |
| `--osx-entitlements-file FILENAME                                   ` | 指定 OS X 应用程序的权限文件.                                     |
| `--runtime-tmpdir PATH                                              ` | 指定运行时临时目录.                                               |
| `--bootloader-ignore-signals                                        ` | 忽略引导加载程序的信号.                                           |
| `--distpath DIR                                                     ` | 指定生成的可执行文件的存储路径.                                   |
| `--workpath WORKPATH                                                ` | 指定工作路径.                                                     |
| `-y                                                                 ` | 自动回答所有提示.                                                 |
| `--upx-dir UPX_DIR                                                  ` | 指定 UPX 的安装路径.                                              |
| `--clean                                                            ` | 清理临时文件.                                                     |
| `--log-level LEVEL                                                  ` | 指定日志级别.                                                     |

## 3. spec 配置文件打包

生成`.spec`配置文件命令 _(通过`2. 命令行打包`方法也会生成`.spec`文件)_

```shell{.line-numbers}
pyi-makespec -n 'dpfwt' 'main.py'
# 生成的文件名称为 dpfwt.spec
```

通过修改`.spec`文件可以对其配置,修改后如下:

```
# -*- mode: python ; coding: utf-8 -*-


a = Analysis(
    ['main.py'],
    pathex=[],
    binaries=[],
    datas=[('resources', 'resources'), ('bin', 'bin')],
    hiddenimports=[],
    hookspath=[],
    hooksconfig={},
    runtime_hooks=[],
    excludes=[],
    noarchive=False,
)
pyz = PYZ(a.pure)

exe = EXE(
    pyz,
    a.scripts,
    [],
    exclude_binaries=True,
    name='dpfwt',
    debug=False,
    bootloader_ignore_signals=False,
    strip=False,
    upx=True,
    console=False,
    disable_windowed_traceback=False,
    argv_emulation=False,
    target_arch=None,
    codesign_identity=None,
    entitlements_file=None,
    icon=['风机.ico'],
)
coll = COLLECT(
    exe,
    a.binaries,
    a.datas,
    strip=False,
    upx=True,
    upx_exclude=[],
    name='dpfwt',
)
```

### 3.1 `spce`配置文件部分参数说明

```
Analysis类:用于分析要打包的Python代码.
    scripts:用于指定要打包的Python文件的列表,例如:['script1.py', 'script2.py'].
    pathex:要搜索模块的路径列表.可以是绝对路径或相对路径.例如:pathex=['/path/to/modules', 'relative/path/to/modules'].
    binaries:要包含在可执行文件中的二进制文件列表.可以是绝对路径或相对路径.例如:binaries=['/path/to/binary1', 'relative/path/to/binary2'].
    datas:要包含在可执行文件中的数据文件列表.每个数据文件是一个元组,包含源文件路径和目标文件路径.例如:datas=[('/path/to/source/file', 'relative/path/to/target/file')].
    hiddenimports:需要显式导入的模块列表.例如:hiddenimports=['module1', 'module2'].
    hookspath:包含自定义钩子的路径列表.可以是绝对路径或相对路径.例如:hookspath=['/path/to/hooks', 'relative/path/to/hooks'].
    hooksconfig:自定义钩子的配置字典.例如:hooksconfig={'hook1': 'config1', 'hook2': 'config2'}.
    runtime_hooks:运行时钩子列表.例如:runtime_hooks=['hook1', 'hook2'].
    excludes:要排除的模块列表.例如:excludes=['module1', 'module2'].
    noarchive:是否禁用打包成归档文件（默认为False）.例如:noarchive=True.

PYZ类:用于生成Python字节码.
    pure:Analysis对象的pure属性,用于生成Python字节码.

EXE类:用于生成可执行文件.
    pyz:PYZ对象,用于生成Python字节码.
    scripts:要执行的脚本列表.例如:scripts=['script1.py', 'script2.py'].
    exclude_binaries:是否排除二进制文件（默认为True）.例如:exclude_binaries=False.
    name:生成的可执行文件的名称.例如:name='my_program'.
    debug:是否启用调试模式（默认为False）.例如:debug=True.
    bootloader_ignore_signals:是否忽略引导程序的信号（默认为False）.例如:bootloader_ignore_signals=True.
    strip:是否去除调试信息（默认为False）.例如:strip=True.
    upx:是否使用UPX压缩可执行文件（默认为True）.例如:upx=False.
    console:是否在控制台中运行程序（默认为False）.例如:console=True.
    disable_windowed_traceback:是否禁用窗口化的回溯（默认为False）.例如:disable_windowed_traceback=True.
    argv_emulation:是否模拟命令行参数（默认为False）.例如:argv_emulation=True.
    target_arch:目标架构（默认为None）.例如:target_arch='x86'.
    codesign_identity:代码签名标识（默认为None）.例如:codesign_identity='my_identity'.
    entitlements_file:授权文件（默认为None）.例如:entitlements_file='entitlements.plist'.
    icon:生成的可执行文件的图标.例如:icon=['my_icon.ico'] , icon='my_icon.ico'.

COLLECT类:用于生成最终的可执行文件.
    exe:EXE对象,用于生成可执行文件.
    binaries:要包含在可执行文件中的二进制文件列表.
    datas:要包含在可执行文件中的数据文件列表.
    strip:是否去除调试信息（默认为False）.
    upx:是否使用UPX压缩可执行文件（默认为True）.
    upx_exclude:要排除的UPX压缩文件列表.
    name:生成的可执行文件的名称.
```

## 4. 附录

### 4.1 文件结构

```
📦dpfwt
 ┣━ 📁.git
 ┣━ 📁.vscode
 ┣━ 📁apps
 ┣━ 📁bin
 ┣━ 📁build           # 生成的中间文件,存储了打包过程中的问题和信息
 ┣━ 📁dist            # 生成的分发文件,最终可执文件及依赖文件位置
 ┣━ 📁docs
 ┣━ 📁resources
 ┣━ 📁tools
 ┣━ 📁__pycache__
 ┣━ 📜.gitignore
 ┣━ 📜dpfwt.spec      # 生成的.spec 文件
 ┣━ 📜main.py
 ┣━ 📜README.md
 ┣━ 📜requirements.txt
 ┣━ 📜test.py
 ┣━ 📜Window.py
 ┗━ 📜风机.ico
```
