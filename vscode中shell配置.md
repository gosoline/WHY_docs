<!-- @format -->

# vscode 中配置 shell 提示补全,语法检查,格式化

## 1. shell 提示补全

vscode 扩展搜索`shellman`,安装扩展

扩展:
![图 shellman](images/vscode中shell配置/shellman.png)
效果:
![图 补全示例](images/vscode中shell配置/补全示例.png)

## 2. shell 语法检查

vscode 扩展搜索`ShellCheck`,安装扩展

扩展:
![图 shellcheck](images/vscode中shell配置/shellcheck.png)
效果:
![图 检查示例](images/vscode中shell配置/检查示例.png)

## 3. shell 格式化

vscode 扩展搜索`shell-format`,安装扩展

扩展:
![图 shfmt](images/vscode中shell配置/shfmt.png)

前往 github 下载`https://github.com/mvdan/sh/releases`对应版本

![图 shfmt版本](images/vscode中shell配置/shfmt版本.png)
复制完整的可执行程序路径
![图 shfmt路径](images/vscode中shell配置/shfmt路径.png)
在 vscode`setting.json`添加设置

```json
"[shellscript]": {
    "editor.defaultFormatter": "foxundermoon.shell-format"
},
// 添加刚才复制的可执行程序路径
"shellformat.path": "D:\\WHYsoftware\\shfmt\\shfmt_v3.7.0_windows_386.exe"
```

![图 配置shfmt路径](images/vscode中shell配置/配置shfmt路径.png)

还有一些细节根据自己需要调整就行.

END
