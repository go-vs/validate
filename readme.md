# Validate

Tired of super long long struct tags? Use this instead

## Install

```shell
go get -u github.com/go-vs/validate
```

## Usage

```go
package main

import (
	. "github.com/go-vs/validate"
	"log"
)

type TestStruct struct {
	A interface{}
	B int64
	C []TestStruct
}

func main() {
	data := TestStruct{
		A: "abcde",
		B: 100,
		C: []TestStruct{
			{
				A: "Hello",
				B: 123,
			},
			{
				A: 123,
				B: 123,
			},
		},
	}

	if err := Use(data, Struct(
		WithKey("some key here"),
		Field("A", Require, MinLength(5)),
		Field("B", Require),
		Field("C", Array(Each(Struct(
			Field("A", String()),
		)))),
	)).Validate(); err != nil {
		log.Fatal(err)
	}
}
```

## Document

### Config

```
SetIncludeErrPath(value bool)
```

### Validator

* [Common](doc/common.md)
* [Array](doc/array.md)
* [Conditional](doc/conditional.md)
* [Number](doc/number.md)
* [String](doc/string.md)
* [Struct](doc/struct.md)
