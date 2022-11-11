# 优雅退出

```go
package main

import (
	"fmt"
	"os"
	"os/signal"
	"syscall"
)

func main() {

	// gin web server

	// 如果接收到 kill 信号
	quit := make(chan os.Signal)
	signal.Notify(quit, syscall.SIGINT, syscall.SIGTERM)
	<-quit

	// 处理后续的逻辑
	fmt.Println("关闭 server 中...")
	fmt.Println("注销服务...")
}
```
