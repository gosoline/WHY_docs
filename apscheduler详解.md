<!-- @format -->

# apscheduler 详解

## 安装

## 四个基本对象

## 使用方法

###

```python {.line-numbers}
from time import sleep

import pandas as pd
from apscheduler.executors.pool import ProcessPoolExecutor, ThreadPoolExecutor
from apscheduler.schedulers.background import BackgroundScheduler
from apscheduler.triggers.interval import IntervalTrigger


def task():
    for i in range(5):
        print(i)
        sleep(1)


if __name__ == '__main__':

    scheduler = BackgroundScheduler(executors={
        'default': ThreadPoolExecutor(),
        'processpool': ProcessPoolExecutor()
    })

    scheduler.add_job(
        func=task,
        trigger=IntervalTrigger(seconds=12,
                                start_date=pd.Timestamp.now() +
                                pd.Timedelta('5s')),
        executor='processpool',
    )

    scheduler.start()
    while True:
        print(pd.Timestamp.now() + pd.Timedelta('5s'))
        sleep(5)

```

```python {.line-numbers}
from time import sleep

from apscheduler.executors.pool import ThreadPoolExecutor
from apscheduler.schedulers.background import BackgroundScheduler
from apscheduler.triggers.interval import IntervalTrigger

i = 0


def task_1():
    global i
    i = i + 1
    while True:
        sleep(1)
        print(i)


scheduler_1 = BackgroundScheduler(executors={
    'tpx_1': ThreadPoolExecutor(2),
    'tpx_2': ThreadPoolExecutor(3)
})
scheduler_1.add_job(
    task_1,
    trigger='interval',
    seconds=5,
    max_instances=3,
    executor='tpx_1',
)
scheduler_1.add_job(
    task_1,
    trigger='interval',
    seconds=7,
    max_instances=3,
    executor='tpx_1',
)
scheduler_1.start()

while True:
    # 获取任务列表
    jobs = scheduler_1.get_jobs()
    print(jobs)
    sleep(3)

```

```python {.line-numbers}
from time import sleep

from apscheduler.events import (EVENT_JOB_ERROR, EVENT_JOB_EXECUTED,
                                JobExecutionEvent)
from apscheduler.schedulers.background import BackgroundScheduler

retval_1 = 0
retval_2 = 0


def listener(event: JobExecutionEvent):
    global retval_1, retval_2
    event.job_id
    if not event.exception:
        if event.job_id == 'job1':
            retval_1 = event.retval
        if event.job_id == 'job2':
            retval_2 = event.retval


def work(name):
    sleep(3)
    return name


if __name__ == "__main__":
    scheduler = BackgroundScheduler()
    scheduler.add_listener(listener, EVENT_JOB_EXECUTED | EVENT_JOB_ERROR)
    scheduler.add_job(work, 'interval', args=('job1_', ), seconds=4, id='job1')
    scheduler.add_job(work, 'interval', args=('job2_', ), seconds=7, id='job2')
    scheduler.start()

    while True:
        print("return value 1: ", retval_1)
        print("return value 2: ", retval_2)
        sleep(1)

```
