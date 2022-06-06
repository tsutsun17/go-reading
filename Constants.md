## Constants

boolean, rune, integer, floating-point, complex, string

rule, integer, floating-point, complex <- "numeric constants"

定数の表し方
rune, integer, floating-point, imaginary, string Literal - (constant expression) -> constant

or

some built-in functions <- ex) unsafe.Sizeof(???certain values), cap or len (applied some expressions), real or imag (applied to a complex constant), complex (applied to numeric constants)

boolean: true, false
iota: integer constant

numeric constants は精度も決める <- overflow しない
<- それゆえ, negative zero, infinity, not-a-number value はない

constant は

- typed
- untyped: literal, true, false, iota, certain constant expressions(const XXX = XXXX, 型づけなし)

> If the type is a type parameter, the constant is converted into a non-constant value of the type parameter.

これやばそう
下のやつだった

```go
package main

import (
	"fmt"
)

func P[T ~float32 | ~float64]() {
	// const: OK
	const C = float32(1.1) + 1.2 // float32(1.1): constant
	fmt.Println(C)

	// const
	const A = T(1.1) + 1.2 // T(1.1): not constant
	fmt.Println(A)

	// var
	B := T(1.1) + 1.2
	fmt.Println(B)
}

func main() {
	P[float32]()
	P[float64]()
}

```

定数は定数どうしの加算や算術しか受け付けない(変数の代入とかできない) <- コンパイル時に値がわかっていないと行けないため

> The default type of an untyped constant is bool, rune, int, float64, complex128 or string respectively

numeric だと, 精度がコンパイラの内部できまる

定数に interface 型を入れることはできない

<- コンパイル時に値が決まらないため

-> interface は変数でしか扱えない([Variables.md](./Variables.md) へ)
