<!-- @format -->

# logging 库用法详解

`logging`模块是 Python 标准库中用于记录日志信息的模块.它提供了灵活的日志记录功能,可以将日志输出到不同的目标（如文件、终端等）,并支持不同级别的日志记录（如调试、信息、警告、错误等）.

## 1. 基本概念

下面是`logging`模块的一些常用概念和用法:

1. Logger（记录器）:`Logger`对象是主要的接口,用于向应用程序代码暴露记录日志的方法.您可以创建自己的`Logger`对象,也可以使用默认的根`Logger`对象.

2. Handler（处理器）:`Handler`对象用于指定日志的输出目标,可以将日志记录到文件、终端、网络等不同的位置.`Handler`对象可以添加到`Logger`对象中,以处理相应级别的日志消息.

3. Formatter（格式化器）:`Formatter`对象用于指定日志消息的输出格式.您可以自定义日志消息的显示方式,包括日期、时间、日志级别、消息内容等.

4. Level（级别）:`Level`对象用于指定日志消息的级别,包括调试（DEBUG）、信息（INFO）、警告（WARNING）、错误（ERROR）等级别.可以根据需要设置适当的级别,以控制日志的输出.

## 2. 代码示例

下面是一个简单的示例,演示如何使用`logging`模块记录日志信息:

```python {.line-numbers}
import logging

# # 配置日志输出到文件,创建一个Logger对象
# # ps:下面的输出到文件功能一样,这里设置了,下面就不需要设置FileHandler对象
# logging.basicConfig(
#     filename='output.txt',
#     level=logging.INFO,
# )
# logger = logging.getLogger(__name__)

# 创建一个Logger对象
logger = logging.Logger(__name__)

# 创建一个Formatter对象,指定日志消息的格式
format = '%(asctime)s - %(levelname)s - %(message)s'
formatter = logging.Formatter(format)

# 创建一个FileHandler对象,将日志输出到文件
file_handler = logging.FileHandler('output.txt')
# 设置日志等级
file_handler.setLevel(logging.INFO)
# 将Formatter对象添加到Handler对象中
file_handler.setFormatter(formatter)
# 将Handler对象添加到Logger对象中
logger.addHandler(file_handler)

# 创建一个StreamHandler对象,将日志输出到终端
console_handler = logging.StreamHandler()
# 设置日志等级
console_handler.setLevel(logging.INFO)
# 将Formatter对象添加到Handler对象中
console_handler.setFormatter(formatter)
# 将Handler对象添加到Logger对象中
logger.addHandler(console_handler)

# 输出日志信息
logger.debug('This is a debug message')
logger.info('This is an info message')
logger.warning('This is a warning message')
logger.error('This is an error message')
logger.critical('This is a critical message')
```

执行后文件和终端输出信息如下:

```
2023-12-23 16:54:22,117 - INFO - This is an info message
2023-12-23 16:54:22,118 - WARNING - This is a warning message
2023-12-23 16:54:22,119 - ERROR - This is an error message
2023-12-23 16:54:22,120 - CRITICAL - This is a critical message
```

## 3. 代码解析

下面是对代码的详细解释:

1. 首先,我们导入了 logging 模块,它是 Python 内置的用于记录日志的模块.

2. 创建一个 Logger 对象,通过`logging.Logger(__name__)`来创建.Logger 对象是日志记录器的核心组件,它负责处理和分发日志消息.

3. 创建一个 Formatter 对象,用于指定日志消息的格式.在这个例子中,我们使用了一个包含时间戳、日志级别和消息的字符串格式.

4. 创建一个 FileHandler 对象,将日志输出到文件.FileHandler 是一个 Handler 的子类,它负责将日志消息写入文件中.我们通过`logging.FileHandler('output.txt')`来创建一个 FileHandler 对象,并将日志输出到名为'output.txt'的文件中.

5. 设置 FileHandler 的日志等级,通过`file_handler.setLevel(logging.INFO)`来设置日志等级为 INFO.这意味着只有 INFO 级别及以上的日志消息才会被记录到文件中.

6. 将 Formatter 对象添加到 FileHandler 对象中,通过`file_handler.setFormatter(formatter)`来设置.

7. 将 FileHandler 对象添加到 Logger 对象中,通过`logger.addHandler(file_handler)`来添加.

8. 创建一个 StreamHandler 对象,将日志输出到终端.StreamHandler 是 Handler 的另一个子类,它负责将日志消息输出到标准输出流（终端）.我们通过`logging.StreamHandler()`来创建一个 StreamHandler 对象.

9. 设置 StreamHandler 的日志等级,通过`console_handler.setLevel(logging.INFO)`来设置日志等级为 INFO.

10. 将 Formatter 对象添加到 StreamHandler 对象中,通过`console_handler.setFormatter(formatter)`来设置.

11. 将 StreamHandler 对象添加到 Logger 对象中,通过`logger.addHandler(console_handler)`来添加.

12. 最后,我们使用 Logger 对象来输出不同级别的日志消息.通过`logger.debug()`、`logger.info()`、`logger.warning()`、`logger.error()`和`logger.critical()`来输出不同级别的日志消息.这些消息将根据设置的日志等级被记录到文件和终端中.

**总结:** 这段代码配置了一个 Logger 对象,将日志消息同时输出到文件和终端.通过设置不同的 Handler 和日志等级,可以灵活地控制日志的输出方式和级别.
