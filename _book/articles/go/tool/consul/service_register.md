# 服务注册

```go
package main

import (
    "github.com/hashicorp/consul/api"
)

func Register(address string, port int, name string, tags []string, id string) error {
    cfg := api.DefaultConfig()
    cfg.Address = "192.168.1.103:8500"

    client, err := api.NewClient(cfg)
    if err != nil {
        panic(err)
    }

    // 生成对应的检查对象
    check := &api.AgentServiceCheck{
        HTTP: "http://127.0.0.1:8021/health",
        Timeout: "5s",
        Interval: "5s",
        DeregisterCriticalServiceAfter: "10s",
    }

    // 生成注册对象
    registration := new(api.AgentServiceRegistration)
    registration.Name = name
    registration.ID = id
    registration.Port = port
    registration.Tags = tags
    registration.Address = address
    registration.Check = check

    err = client.Agent().ServiceRegister(registration)
    if err != nil {
        panic(err)
    }

    return nil
}

func main() {
    _ := Register("192.168.1.102", 8021, "user_web", []string{"web"}, "user_web")
}
```
