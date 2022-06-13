### Types

Composite types: array, struct, pointer, function, interface, slice, map, channel


#### Numeric Types
byte: uintのalias
rune: inte32のalias

#### String Types

Stringsはimmutable: once created
```go
package main

import (
	"fmt"
	"reflect"
)

func main() {
	s := "abcde"
	//	&s[1] = "w"  // NG
	fmt.Println(reflect.TypeOf(s[1])) // uint8
	fmt.Println(reflect.TypeOf(s))    // string
    	fmt.Println(s[1])		      // 98
}
```

#### Array Types








