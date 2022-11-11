# viper

```yaml:config.yaml
name: 'fmw'
port: 8021
```

```go
package main

import (
    "fmt"
    "github.com/spf13/viper"
)

type ServerConfig struct {
    ServiceName string `mapstructure:"name"`
    ServicePort int `mapstructure:"port"`
}

func main() {
    v := viper.New()
    v.SetConfigFile("config.yaml")
    if err := v.ReadInConfig(); err != nil {
        panic(err)
    }
    fmt.Println(v.Get("name"))

    serverConfig := ServerConfig{}
    if err := v.Unmarshal(&serverConfig); err != nil {
        panic(err)
    }
    fmt.Println(serverConfig)
}
```