# ini

```ini:config.ini
[app]
DefaultPage = 1
DefaultPageSize = 10

[db]
Host = 127.0.0.1
Port = 3306
User = root
Password = 123456
```

```go
package config

import (
	"fmt"
	"time"

	"github.com/go-ini/ini"
)

type App struct {
	DefaultPage     string
	DefaultPageSize string
}

var AppSetting = &App{}

type Database struct {
	Host     string
	Port     string
	User     string
	Password string
	Url      string
}

var DatabaseSetting = &Database{}

var cfg *ini.File

func init() {
	var err error
	cfg, err = ini.Load("config.ini")
	if err != nil {
		fmt.Printf("Fail to read file: %v", err)
	}

	mapTo("app", AppSetting)
	mapTo("db", DatabaseSetting)

	DatabaseSetting.Url = fmt.Sprintf("%s:%s@tcp(%s:%s)/%s?charset=utf8mb4&parseTime=True&loc=Local",
		DatabaseSetting.User,
		DatabaseSetting.Password,
		DatabaseSetting.Host,
		DatabaseSetting.Port,
		DatabaseSetting.Name,
	)
}

func mapTo(section string, v interface{}) {
	err := cfg.Section(section).MapTo(v)
	if err != nil {
		panic(err)
	}
}
```
