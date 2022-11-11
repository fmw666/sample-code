# zap

## 安装

```
go get go.uber.org/zap
```

## 使用

### 快速使用

```go
package main

import (
    "time"

    "go.uber.org/zap"
)

func main() {
    logger := zap.NewExample()
    defer logger.Sync()

    url := "http://example.org/api"
    logger.Info("failed to fetch URL",
        zap.String("url", url),
        zap.Int("attempt", 3),
        zap.Duration("backoff", time.Second),
    )

    sugar := logger.Sugar()
    sugar.Infow("failed to fetch URL",
        "url", url,
        "attempt", 3,
        "backoff", time.Second,
    )
    sugar.Infof("Failed to fetch URL: %s", url)
}
```

### 输出到文件

```go
package main

import (
    "time"

    "go.uber.org/zap"
)

func NewLogger() (*zap.Logger, error) {
    cfg := zap.NewProductionConfig()
    cfg.OutputPaths = []string{
        "./myproject.log",
    }
    return cfg.Build()
}

func main() {
    logger, err := NewLogger()
    if err != nil {
        panic(err)
    }

    sugar := logger.Sugar()
    defer sugar.Sync()
    url := "http://example.org/api"
    sugar.Info("failed to fetch URL",
        zap.String("url", url),
        zap.Int("attempt", 3),
        zap.Duration("backoff", time.Second),
    )
}
```

### 全局变量

```go

package main

import (
    "go.uber.org/zap"
)

func main() {
    logger, _ := NewDevelopment()
    zap.ReplaceGlobals(logger)

    zap.S().Debug("Hello")
}
```
