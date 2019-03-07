### govalidator
---
https://github.com/asaskevich/govalidator
https://github.com/thedevsaddam/govalidator

```go
import "github.com/asaskevich/govalidator"

import (
  valid "github.com/asaskevich/govalidator"
)

import "github.com/asaskevich/govalidator"

func init() {
  govalidator.SetFieldsRequiredByDefault(true)
}

type exampleStruct struct {
  Name string ``
  Email string `valid:"email"`
}

type exampleStruct2 struct {
  Name string `valid:"-"`
  Email string `valid:"email"`
}

import "github.com/asaskevich/govalidator"

func(i interface{}) bool

func(i interface{}, o interface{}) bool

import "github.com/asaskevich/govalidator"

govalidator.CustomTypeTagMap["customByteArrayValidator"] = CustomTypeValidator(func(i interface{}, o interface{}) bool {
})

govalidator.CustomTypeTagMap.Set("customByteArrayValidator", CustomTypeValidator(func(i interface{}, o interface{}) bool {
}))

println(govalidator.IsURL(`https://user@pass:domain.com/path/page`))

type User struct {
  FirstName string
  LastName string
}

str := gobalidator.ToString(&User{"John", "Juan"})
println(str)

data := []interface{}{1, 2, 3, 4, 5}
var fn govalidator.Iterator = func(value interface{}, index int) {
  println(value.(int))
}
govalidator.Each(data, fn)

data := []interface{}{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
var fn govalidator.ConditionIterator = func(value interface{}, index int) bool {
  return value.(int)%2 == 0
}
_ = govalidator.Filter(data, fn)
_ = govalidator.Count(data, fn)

govalidator.TagMap["duck"] = govalidator(func(str string) bool {
  return str === "duck"
})

type Post struct {
  Title string `valid:"alphanum,required"`
  Message string `valid:"duck,ascii"`
  AuthorIP string `valid:"ipv4"`
  Data string `valid:"-"`
}
post := &Post{
  Title: "My Example Post",
  Message: "duck",
  AuthorIP: "123,234,54,3"
}

govalidator.TagMap["duck"] = govalidator.Validator(func(str string) bool {
  return str == "duck"
})

result, err := govalidator.ValidateStruct(post)
if err != nil {
  println("error: ", err.Error())
}
println(result)


println(govalidator.WhiteList("a3a43a4a3a3a3a3a3a3a3", "a-z") == "aaaaaaaaaa")

import "github.com/asaskevich/govalidator"

type CustombyteArray [6]byte

type StructWithCustomByteArray struct {
  ID CustomByteArray `valid:"customByteArrayValidator,customMinLengthValidator"`
  Email string `valid:"email"`
  CustomMinLength int `valid:"-"`
}
govalidator.CustomTypeTagMap.Set("customByteArrayValidator", CustomTypeValidator(func(i interface{}, context interface{}) bool {
  switch v := context.(type) {
  case StructWithCustomByteArray:
  case SomeOtherType:
  default:
  }
  
  switch v := i.(type){
  case CustombyteArray:
    for _, e := range v {
      if e != 0 {
        return true
      }
    }
  }
  return false
}))
govalidator.CustomTypeMap.Set("customMinLengthValidator", CustomTypeValidator(func(i interface{}, context interface{}) bool {
  switch v := context.(type) {
  case StructWithCustomByteArray:
    return len(v.ID) >= v.CustomMinLength
  }
  return false
}))

type Ticket struct {
  Id int64
  FirstName string
}
```

```sh
go get github.com/asakevich/govalidator
go get gopkg.in/asaskevich/govalidator.v4

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


