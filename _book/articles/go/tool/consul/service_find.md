# 服务查找

```go
package main

import (
    "fmt"
    "github.com/hashicorp/consul/api"
)

func AllServices() {
    cfg := api.DefaultConfig()
    cfg.Address = "192.168.1.103:8500"

    client, err := api.NewClient(cfg)
    if err != nil {
        panic(err)
    }

    data, err := client.Agent().Services()
    // data, err := client.Agent().ServicesWithFilter(`Service == "user_web"`)
    if err != nil {
        panic(err)
    }
    for key, _ := range data {
        fmt.Println(key)
    }
}
```
