<!-- @format -->

# vscode 替换变量

本文仅为部分翻译,详情见 vscode 官方文档:[vscode 官网替换变量解释][1]

## 预定义变量

支持以下预定义变量:

```{.line-numbers}
${userHome} - 用户家目录的路径
${workspaceFolder} - 在 VS Code 中打开的文件夹的路径
${workspaceFolderBasename} - 在 VS Code 中打开的文件夹的名称,不包括任何斜杠(/)
${file} - 当前打开的文件
${fileWorkspaceFolder} - 当前打开的文件所在的工作区文件夹
${relativeFile} - 相对于 workspaceFolder 的当前打开文件
${relativeFileDirname} - 相对于 workspaceFolder 的当前打开文件的目录名
${fileBasename} - 当前打开文件的基本名称
${fileBasenameNoExtension} - 不带文件扩展名的当前打开文件的基本名称
${fileExtname} - 当前打开文件的扩展名
${fileDirname} - 当前打开文件的文件夹路径
${fileDirnameBasename} - 当前打开文件的文件夹名称
${cwd} - VS Code 启动时任务运行器的当前工作目录
${lineNumber} - 活动文件中当前选定的行号
${selectedText} - 活动文件中当前选定的文本
${execPath} - 运行中的 VS Code 可执行文件的路径
${defaultBuildTask} - 默认构建任务的名称
${pathSeparator} - 操作系统用于在文件路径中分隔组件的字符
```

## 预定义变量示例

一个文件位于 `/home/your-username/your-project/folder/file.ext`,并在您的编辑器中打开；
目录 `/home/your-username/your-project` 作为根工作区打开.

那么每个变量将具有以下值:

```{.line-numbers}
${userHome} - /home/your-username
${workspaceFolder} - /home/your-username/your-project
${workspaceFolderBasename} - your-project
${file} - /home/your-username/your-project/folder/file.ext
${fileWorkspaceFolder} - /home/your-username/your-project
${relativeFile} - folder/file.ext
${relativeFileDirname} - folder
${fileBasename} - file.ext
${fileBasenameNoExtension} - file
${fileDirname} - /home/your-username/your-project/folder
${fileExtname} - .ext
${lineNumber} - 光标所在行号
${selectedText} - 代码编辑器中选定的文本
${execPath} - Code.exe 的位置
${pathSeparator} - 在 macOS 或 Linux 上是 /,在 Windows 上是 \
```

[1]: https://code.visualstudio.com/docs/editor/variables-reference#_environment-variables
