# 闰年判断

普通闰年：可以被 4 整除，不能被 100 整除

世纪闰年：可以被 400 整除

闰年天数：366天

```go
package main

import (
    "fmt"
)

func main() {
    var year int = 2022
    if (year % 4 == 0 && year % 100 != 0) || year % 400 == 0 {
        fmt.Println("是闰年")
    } else {
        fmt.Println("不是闰年")
    }
}
```
