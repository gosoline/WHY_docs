<!-- @format -->

# 代码超时检测

## 1. 使用 `func_timeout` 库

### 1.1 下载 `func_timeout`库

```shell {.line-number}
pip install func_timeout
```

### 1.2 示例

> **注意**
> 使用该库时被检测函数需要是可中断的,此时超时时可以及时抛出超时异常,并中断线程,但是在示例中 `time.sleep` 调用会挂起当前线程,使得它在指定的时间内不会执行任何操作.如果在主线程中调用 `fc`,这会导致主线程挂起.
>
> 然而,`func_timeout` 通过在另一个线程或进程中运行给定的函数来工作.如>果函数运行时间超过了指定的超时时间,它会尝试中止执行并抛出异常.
>
> 在示例代码中,即使 `func_timeout` 在 3 秒后抛出了 `FunctionTimedOut` 异常,但是由于 `fc` 函数中的 `time.sleep(10)` 调用,该函数所在的线程可能仍然在休眠.由于异常是在 `fc` 函数的线程外部抛出的,所以不会影响 `time.sleep` 的执行.`time.sleep` 会继续执行直到完成,即使 `func_timeout` 已经报告了超时.
>
> 因此该示例会在运行约 10 秒后才会抛出超时异常

```python {.line-numbers}
import time

from func_timeout import func_timeout, FunctionTimedOut


def fc():
    time.sleep(10)  #模拟耗时操作


start = time.time()
try:
    func_timeout(3, fc)
except FunctionTimedOut:
    print(f'在运行{time.time() - start}秒后报错')  # 约10秒
```

## 2. 自定义超时函数

### 2.1 自定义函数 `run_with_timeout`

```python {.line-numbers}
import threading


# 自定义超时错误类型
class TimeoutError(Exception):
    pass


def run_with_timeout(
        timeout_seconds: float,
        func,
        args: tuple = (),
        kwargs: dict = {},
):
    '''
    ~监视函数是否超时,未超时返回函数结果,超时抛出`TimeoutError`异常

    Parameters
    ----------
    - timeout_seconds: 超时秒数
    - func: 所检测的函数
    - args: 所检测函数位置参数
    - kwargs: 所检测函数关键字参数
    '''

    result = []
    event = threading.Event()

    def _code_wrapper():
        try:
            result.append(func(*args, **kwargs))
        except Exception as e:
            result.append(e)
        event.set()

    thread = threading.Thread(target=_code_wrapper)
    thread.start()
    event.wait(timeout_seconds)
    if event.is_set():
        thread.join()
        if isinstance(result[0], Exception):
            raise result[0]
        else:
            return result[0]
    else:
        raise TimeoutError(
            f'Function {str(func)} (args={args}) (kwargs={kwargs}) timed out after {timeout_seconds} seconds.'
        )
```

### 2.2 示例

> **注意**
> 该程序会在约 3 秒后抛出超时异常,但是 `fc` 函数并不会被中断而是继续运行

```python {.line-numbers}
import time


def fc():
    time.sleep(10)  #模拟耗时操作


start = time.time()
try:
    run_with_timeout(3, fc)
except TimeoutError:
    print(f'在运行{time.time() - start}秒后报错')  # 约3秒

```
