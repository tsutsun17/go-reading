#### Type Inference
関数の型パラを持った関数の引数の型推論の話

Each step attempts to use known information to infer additional type arguments.
型推論は全ての型Argumentの方がわかったら終わる

なんかチェック入って、型制約が満たされていなかったらインスタンス化は失敗する
型推論は
- 型パラリスト
- 既知の型引数で初期化された置換マップM(もしあれば)
- 通常の関数引数のリスト(関数呼び出しの場合のみ)
に基づく

1. 全て型づき普通の関数引数に、関数引数の型推論を行う(var int a = 1とかを入れる)
2. 制約条件の型推論を適用する
3. 型づけされていない普通の関数引数に対して、片付けされていない関数引数(1.1とかをそのまま入れちゃう)それぞれのデフォルトの型を使って関数引数の型推論を適用する
4. 制約条件の型推論を適用する

> If there are no ordinary or untyped function arguments, the respective steps are skipped. Constraint type inference is skipped if the previous step didn't infer any new type arguments, but it is run at least once if there are missing type arguments.

普通のもしくは型付でない、関数引数がなかったらこのステップはスキップされる
スキップされたら、制約条件の方もスキップされる
ただし、一つでもmissing type argumentがあれば、実行される

> The substitution map M is carried through all steps, and each step may add entries to M. The process stops as soon as M has a type argument for each type parameter or if an inference step fails. If an inference step fails, or if M is still missing type arguments after the last step, type inference fails.

置換マップMは全てのステップで共通に使われる。
各ステップでは、Mにエントリを入れることができる
このプロセスは、Mが各型パラメータに対する型引数を持つか、推論ステップが失敗すると、すぐに停止する。
推論ステップが失敗した場合、または最後のステップの後でもMに型引数がない場合、型推論は失敗する。

```go
func [Number ~float64 | ~float32] size(vec []Number, n Number) int {
    return len(vec)
}

size(vec, 1.3)

type Number interface {
    ~float32 | ~float64
    sum() int // <- これがあると、推論は成功するけど、インスタンス化はできない
}
```

substitution map は関数呼び出しごとに作られる
スタック的にどんどん型を決めていく

interface: any

untypeはどこで決まる？ => runtimeの環境によって決まる