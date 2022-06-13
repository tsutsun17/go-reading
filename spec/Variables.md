### Variables

interface は dynamic type をとる

> The static type (or just type) of a variable is the type given in its declaration, the type provided in the new call or composite literal, or the type of an element of a structured variable. Variables of interface type also have a distinct dynamic type, which is the (non-interface) type of the value assigned to the variable at run time (unless the value is the predeclared identifier nil, which has no type). The dynamic type may vary during execution but values stored in interface variables are always assignable to the static type of the variable.

```go
    var x interface{} // dynamic
    x = nil
    v := reflect.ValueOf(x)
    fmt.Printf("v.Kind()=%v", v.Kind()) // invalidになる

    x = 1 // OK
    x = "aaa" // OK

    v = reflect.ValueOf(x)
    fmt.Printf("v.Kind()=%v", v.Kind()) // stringになる
```

array, slice, struct type: 要素は変数のように動作

> A variable declaration or, for function parameters and results, the signature of a function declaration or function literal reserves storage for a named variable. Calling the built-in function new or taking the address of a composite literal allocates storage for a variable at run time. Such an anonymous variable is referred to via a (possibly implicit) pointer indirection.

関数のパラメータやレスポンスにおける変数宣言:
関数引数や関数リテラルのシグネチャは名前付き変数のストレージを確保する

built-in 関数(new)や複合リテラルのアドレスの取得: 実行時に変数のストレージを確保する
上のような無名変数についてはポインタ・インダイレクト(ポインタ間参照)によって参照される

ポインタインダイレクト
