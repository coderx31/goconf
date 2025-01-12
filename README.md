# Go Config
Library to load env configuration

### How to use it

```go
package main
import (

"errors"
"github.com/caarlos0/env/v11"
"github.com/wgarunap/goconf"
"log"
)

type Conf struct {
	Name string `env:"MY_NAME"`
}

var Config Conf

func (Conf) Register()error {
	return env.Parse(&Config)
}

func (Conf) Validate() error{
	if Config.Name == "" {
		return errors.New(`MY_NAME environmental variable cannot be empty`)
	}
    return nil
}

func (Conf) Print() interface{} {
	return Config
}

func main() {
	err := goconf.Load(
		new(Conf),
	)
    if err != nil{
           log.Fatal(err)
    }
    log.Print(`configuration loaded, `,Config.Name)
}

```