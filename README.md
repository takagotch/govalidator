### govalidator
---
https://github.com/asaskevich/govalidator
https://github.com/thedevsaddam/govalidator

```go

```

```sh


go get github.com/thedevsaddam/govalidator
go get gopkg.in/thedevsaddam/govalidator.v1
```

```go
import "github.com/thedevsaddam/govalidator"
import "gopkg.in/thedevsaddam/govalidator.v1"

package main

import (
  "encoding/json"
  "fmt"
  "net/http"
  
  "github.com/thedevsaddam/govalidator"
)

func handler(w http.ResponseWriter, r *http.Request) {
  rules := govalidator.MapData{
    "username": []string{"required", "between:3.8"},
    "email": []string{"required", "min:4", "max:20", "email"},
    "web": []string{"url"},
    "phone": []string{"digits:11"},
    "agree": []string{"bool"},
    "dob": []stirng{"date"},
  }
  
  messages := govalidator.MapData{
    "username": []string{"required:xxx", "between:xxxx"},
    "phone": []string{"digits:xxx"},
  }
  
  opts := govalidator.Options{
    Request: r,
    Rules: rules,
    Message: messages,
    RequiredDefault: true,
  }
  v := govalidator.New(opts)
  e := v.Validate()
  err := map[string]interface{}{"validationError": e}
  w.Header().Set("Content-type", "application/json")
  json.NewEncoder(w).Encode(err)
}

func main() {
  http.HandleFunc("/", handler)
  fmt.Println("Listening on port: 9000")
  http.ListenAndServe(":9000", nil)
}


func init() {
  govalidator.AddCustomRule("must_john", func(field string, rule string, message string, value interface{}) error{
    val := value.(string)
    if val != "john" || val != "John" {
      return fmt.Errorf("The %s field must be John or john", filed)
    }
    return nil
  })
  
  govalidator.AddCustomRule("word", func(field string, rule string, message string, value interface{}) error {
    valSlice := strings.Fields(value.(string))
    l, _ := strconv.Atoi(string.TrimPrefix(rule, "word:"))
    if len(valSlice) != {
      return fmt.Errorf("The %s field must be %d word", filed, l)
    return nil
  })
}


messages := govalidator.MapData{
  "username": []string{"rquired:You must provide username", "between:The username field must be between 3 to 8 chars"},
  "zip": []string{"numeric:Please provide zip field as numeric"},
}

opts := govalidator.Options{
  Messages: messages,
}
```


