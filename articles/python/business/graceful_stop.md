# 优雅退出

```py
import sys
import signal


def on_exit(signo, frame):
    print("退出系统")
    sys.exit(0)


if __name__ == "__main__":
	# 主进程退出信号监听
    """
    windows 下支持的信号是有限的：
        SIGINT ctrl+C 终端
        SIGTERM kill 发出的软件终止
    """
    signal.signal(signal.SIGINT, on_exit)
    signal.signal(signal.SIGTERM, on_exit)
```
