<!-- @format -->

# pathlib 模块详解

pathlib 是 Python 中用于处理文件路径的标准库模块.它提供了一种面向对象的方式来操作文件和目录路径,使得处理路径更加简单和直观.

**下面是对 pathlib 模块的详细解释:**

1. 导入模块:首先,导入 pathlib 模块:

```python {.line-numbers}
from pathlib import Path
```

2. 创建路径对象:使用 Path 类创建一个路径对象,可以使用以下方式创建路径对象:

```python {.line-numbers}
path = Path('path/to/file.txt')  # 使用字符串创建路径对象
path = Path.cwd() / 'path' / 'to' / 'file.txt'  # 使用 / 操作符连接路径部分
```

3. 获取路径的属性:可以使用以下方法获取路径的各种属性:

-   `path.name`:获取路径的文件名或目录名
-   `path.stem`:获取路径的文件名（不包含扩展名）或目录名
-   `path.suffix`:获取路径的文件扩展名
-   `path.parent`:获取路径的父目录
-   `path.parents`:获取路径的逻辑祖先的不可变序列,`path.parents[0]`与`path.parent`相同
-   `path.parts`:获取路径的各个部分作为元组
-   `path.is_file()`:检查路径是否为文件
-   `path.is_dir()`:检查路径是否为目录
-   `path.exists()`: 检查路径是否存在
-   `path.absolute()`: 获取路径的绝对路径.它可以将相对路径转换为绝对路径,并返回一个新的 Path 对象
-   `path.resolve()`: 获取路径的规范路径.它可以解析路径中的符号链接,并返回一个表示实际文件系统路径的新的 Path 对象(可以用来判断两个路径是否为为同一个路径)

4. 文件和目录操作:pathlib 提供了一些方法来操作文件和目录,例如创建目录、删除文件等.以下是一些常用的方法:

-   `path.mkdir()`:创建目录
    > _参数解析_
    >
    > -   mode:指定目录的权限模式.它可以是一个整数或一个字符串.默认值为 0o777,表示目录具有最大的权限.你也可以传递一个八进制数值,如 0o755,或者使用字符串形式,如 "755".
    > -   parents:一个布尔值,用于指示是否递归地创建父级目录.如果设置为 True,并且指定的路径中的某些父级目录不存在,那么这些父级目录也会被创建.默认值为 False.
    > -   exist_ok:一个布尔值,用于指示如果目录已经存在时是否抛出异常.如果设置为 True,则不会抛出异常,而是默默地继续执行.如果设置为 False,则如果目录已经存在会抛出一个 FileExistsError 异常.默认值为 False
-   `path.rmdir()`:删除目录
-   > _注意_
    >
    > -   只能删除非空目录,否则会报错,如果要删除非空目录,请使用 `shutil`模块 (`shutil.rmtree(path)`)
-   `path.touch()`:创建文件
-   `path.unlink()`:删除文件

1. 遍历目录:可以使用 `path.iterdir()` 方法来遍历目录下的文件和子目录,返回一个迭代器.可以使用 `path.glob(pattern)` 方法来匹配文件和目录,返回一个生成器.

```python {.line-numbers}
# 注意这里 item,file 都是完整路径而不仅仅是文件或目录名

for item in path.iterdir():
    print(item)

for file in path.glob('*.txt'):
    print(file)
```
