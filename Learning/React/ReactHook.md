## React パフォーマンス向上な方法

#### 始める前に､Reactレンダーのタイミン紹介

- Reactコンポネントは自分のstateが変更された場合､渡されるpropsが変更された場合に再レンダリングされるです｡
- 親コンポネントが再レンダリングされると子コンポネントも一緒に再レンダリングされる｡この時子コンポネントが最適化されていなかったら､親から渡されるpropsに変更がなくても､基本的に再レンダリングされるです｡
- コンポネントが再レンダリングされると､その中に宣言(せんげん)されている関数や変数は以前保存されていたメモリを空けて新しいメモリに再び(ふたたび)保存されるです｡

#### はじめに

- React.memo
- useCallback
- useMemo

#### React.memoとは

React.memoとはコンポネントをメモ化するReactのAPIです｡

```react
const MyComponent = React.memo(function MyComponent(props) {
  /* render using props */
});
```

React.memoを使うことで､propsの値が変わらないなら､関数コンポネントのレンダリングを抑制(よくせい)することができるAPIです｡

そして以下のようなコンポネントをメモ化するとパフォーマンス向上有効できるです｡

- レンダリングが高いコンポネント
- 頻繁(ひんぱん)再レンダリングされるコンポネントの子コンポネント

デフォルトでは props オブジェクト内の複雑なオブジェクトは浅い(あさい)比較のみが行われます(おこなわれます)。比較を制御(せいぎょ)したい場合は 2 番目の引数(ひきすう)でカスタム比較関数を指定できます。

```react
function MyComponent(props) {
  /* render using props */
}
function areEqual(prevProps, nextProps) {
  /*
  nextProps を render に渡した結果が
  prevProps を render に渡した結果となるときに true を返し
  それ以外のときに false を返す
  */
}
export default React.memo(MyComponent, areEqual);
```

#### useCallback とは

一言でいうと､パフォーマンス向上のためのフックです｡

```react
const callback = useCallback(コールバック関数,[依存配列]);
```

[メモ化](https://en.wikipedia.org/wiki/Memoization)されたコールバックを返します(かえします)。その関数は依存配列の要素のいずれかが変化した場合にのみ変化します｡これは､不必要なレンダーを避けるために､参照の同一(どういつ)性を見るよう最適化されたコンポネントにコールバックを渡す場合に便利です｡

#### useMemoとは

`useCallback`同様､パフォーマンス向上のためのHookです｡

```react
const memoizedValue = useMemo(コールバック関数,[依存配列]);
```

`useCallback`の違いは点は：

- `useCallback`は関数自体をメモ化です｡
- `useMemo`は関数の結果をメモ化

`useMemo`は､値を計算するための不要な再計算をスキップすることでパフォーマンス向上させます｡

#### デモ



#### まとめ

パフォーマンス向上対応策の方針

- 必要がないレンダリングのコンポネントは再レンダリングしないように
- レンダリング毎に高価(こうか)な計算が実行されるのを避けること｡

##### 補足

###### メモ化とは

> メモ化（英: Memoization）とは、プログラムの高速化のための最適化技法の一種であり、サブルーチン呼び出しの結果を後で再利用するために保持し、そのサブルーチン（関数）の呼び出し毎の再計算を防ぐ手法である。メモ化は[構文解析](http://d.hatena.ne.jp/keyword/%B9%BD%CA%B8%B2%F2%C0%CF)などでも使われる（必ずしも高速化のためだけとは限らない）。キャッシュはより広範な用語であり、メモ化はキャッシュの限定的な形態を指す用語である。

以上｡

















