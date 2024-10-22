## reactの基本

SPAの場合はページが１つのみ
JSX気泡では関数の返却値としてHTMLタグが記述でき、それをコンペーネントとして扱って画面を構成できる

### JSXのルール
ではh１タグの下にpタグで文字を表示したいとして、
return以降が複数行になる場合は()で囲ってあげる。

1つ重要なルールとしてreturn以降は１つのタグで囲われている必要がある
なので<div>で囲む
もしくはreactに用意されているfragmentというものをimportして使う
これなら空タグで囲めるのでエラーが少なくて済む

##　コンポーネントの使い方
react開発では画面の要素をさまざまな粒度のコンポーネントに分類することで再利用性や保守性を高めるのが基本となる

関数で定義されたコンポーネントを関数コンポーネントという

### コンポーネントの分割
コンポーネント用に関数コンポーネントを書いたApp.jsファイルを用意する。
このままでは他で使えないのでexportする必要がある。
こうすることでimportして使うことができる
例では同階層のApp.jsからAppという名前の関数コンポーネントを読み込むことで元のページでは何も記載がない状態で、importしたファイルの情報を読み込んで表示ができている。

###　コンポーネントファイルの拡張子
jsファイルはjsxにしても動く
コンポーネントファイルは全てこの形式にするといい

##　イベントやスタイルの扱い方

### イベントの扱い方
通常ボタンを押した時のイベントはonclickとするがreactはどうか

ボタンに対してクリックイベントを割り当てるが、reactの場合はイベントなどがキャメルケースになる。
そしてjsxで書かれているHTMLのようなタグの中(return以降など)では{}で囲むことでjavascriptを記述できる
'''
export const App = () => {
  const onClickButton = () => {
    alert();
  };
  return (
    <div>
      <h1>こんにちは！</h1>
      <p>お元気ですか？</p>
      <button onClick={onClickButton}>ボタン</button>
    </div>
  );
};
'''

###　スタイルの扱い方
HTML同様styleタグをつけて適用できる。
注意点としてCSSの各要素はJavascriptのオブジェクトとして記述する。
例えば文字の色を赤色にしたい場合は以下のように、
<h1 style={{ color: "red"}}>こんにちは</h1>

styleを指定し、イベント同様に書くので,style={}のように波括弧で囲みその中にオブジェクトでCSSに対応する要素を指定していくため、style={{}}となる。

オベジェクトでのCSSの指定方法はプロパティ名にCSSの名前を書き”red”のようにしないといけない。
これら2つを踏まえ、
style={{ color: "red"}}
となる。

### props
propsはコンポーネントに渡す引数のようなもので、コンポーネントは受け取ったpropsに応じて表示するスタイルや内容を変化させる。
例えば通常時は黒字でエラー時は赤字にする時、都度コンポーネントを作っては大変なのである程度同的に使いまわせるようにするのがこのprops

### propsの使い方
propsを使うには渡す方と渡される方のファイルを修正する必要がある
渡す方はコンポーネントのタグの中に任意の名前をつけてpropsを渡す
今回は色とメッセージを渡したいのでcolorとmessageとしている。
そして＝の後に実際に渡す値を設定することができる。
今回はcolorとmessageをpropsとして渡す
`<coloredMessage color="blue" message="お元気ですか" />`

その後propsファイルに、
```
export const çoloredMessage = (props) => {
    console.log(props);
```
を追加して

親コンポーネント(App.jsx)から

親コンポーネントの条件をpropsでサブコンポーネントが受け取り、その条件にあうものを返す、かんじ


### children
propsはタグ内で任意の名称を使っていた。
それ以外にも特別なpropsとしてchildrenがある
コンポーネントも通常のHTMLタグと同様以下のように任意の要素を囲って使用できる。
この囲まれた部分をchildrenとして利用できる。
```
//childrenが未設定
<ColoredMessage />

//childrenとしてnushidaを設定
<ColoredMessage>nushida</ColoredMessage>
```
よりわかりやすくなる？らしい（そうか？）
以下childrenでの渡し方
```
//app.jsxを編集
<ColoredMessage color="blue" message="お元気ですか" />
↓
<ColoredMessage color="blue" >お元気ですか?</ColoredMessage>

//childrenでメッセージを受け取る
return <p style={contentStyle}>{props.children}</p>;
```
これで受け取れるようになる
単純な文字列以外にも以下のようなタグで囲んだ要素を丸ごと渡すこともできる
<SomeComponent>
  <div>
    <span>nushida</span>
    <p>sakioka</p>
  </div>
</SomeComponent>

// SomeComponent の　childrenには以下が渡る
<div>
  <span>nushida/</span>
  <p>sakioka</p>
</div>

複雑なコンポーネントを組んでいく場合、必須の知識となる。
childrenは読みやすくし、まとめて送ることもできる。

### propsを扱うテクニック
分割代入とオブジェクトの省略記法を使ったテクニック
先の例だとpropsを扱う場合props.としている
なんでもprops.~と記述するのは大変なので分割代入しておくことで楽できる
```
const{color, children} = props;
const contentStyle = {
  color: color, //props.が不要
  fontSize: "20px"
};

//　Props.が不要
return <p style={contentStyle}>{children}</p>;
```

hajimeni
propsから要素を取り出してそれ以降の記述を短くすることができた。
またPropsを取り出したことによってcontentStyleのcolorはプロパティ名と設定値が同一になったので以下のようにオブジェクトの省略記法に従って短くかける

```
const{color, children} = props;
const contentStyle = {
  color,  //省略記法が使える
  fontSize: "20px"
};
```

他にも引数の段階で展開するパターンモアある
```
export const ColoredMessage = ({ color, children }) => {
  const contentStyle = {
    color,
    fontSize: "20px",
  };

  // props.childrenに変更
  return <p style={contentStyle}>{children}</p>;
};

```

## State(useState)
React開発では画面に表示するデータや可変の状態をStateとして管理していく
最も大切なところ。

### Stateとは
webアプリにはさまざまな状態がある。
エラーはあるか、モーダルウィンドウは開いているか、ボタンは押せるか...など
このような状態全てはstateとして管理し、イベントの実行時に更新処理を行うことで動的アプリケーションを実現していきます。

### useState
現在主流になっている関数コンポーネントではReact Hooksと総称される機能群のuseStateという関数を用いてstateを扱っている
使用するためにはReactのimportが必要
`import {useState} from "react";`

useState関数の返却値は配列の形で１つ目にState変数、２つ目にそのStateを更新するための関数が設定されている。
`const [num, setNum]= useState();`
この場合はnumが状態をもった変数、setNUmがそれを更新する関数となる
そしてuseStateは関数なので使用するときは()をつけて関数を実行しよう
分割代入で名称は自由だが基本的に変数名がnumならsetNumのようにする上記の場合はnumの初期値はundifinedになる。state変数に初期値を設定したいケースも多々あるのでその場合はuseState関数を実行する際に引数を指定する。
`const [num, setNum] = useState(0);`
↑これがstate初期値設定のテンプレ

このように値を指定することでStateの初期値を制御できます。
これをApp .ajxに数値のStateを定義し画面に表示、ボタン押下時にカウントアップする機能を実装してみましょう
```
import {useState} from "React"

//Stateの定義
const[num, setNum] = useState(0);

//ボタンを押したときにStateをカウントアップ
const onClickButton = () => {
  setNum(num + 1);
};

<p>{num}</p>
```
ボタン押下時にsetNum関数でStateの値を+1しているので、画面に表示したStateの値がカウントアップされている
数値以外にもjavascriptで変数として扱う「文字列」「真偽値」「配列」「オブジェクト」などなんでもStateとして管理できる
もっと掘り下げた具体的なStateの使い方は後続の章で順次紹介していく。
これだけしかないのはなんか拍子抜けだな

### 厳密には
setNum(num + 1)みたいに書いてカウントアップを実装したが厳密には正しくない
いまのstateの値に基づいてstateを更新するときはset関数内で関数を指定するといい
`setNum((prev) => prev + 1);`

カッコ内に関数をかくとその関数の引数に「更新直前の
そのStateの値」が渡されるからその値に1を足すことで同じことが実現できる。
こう書いた方が本当の意味で直前の関数にプラ一できるぞとのことd

##　再レンダリングと副作用（useEffect）
ここまでPropsとStateを解説してきました。
これに加えて章題について解説

### 再レンダリング
先ほどのカウントアップでは画面が更新されていないのに数字が上昇して行った。これはコンポーネントの再レンダリングされているため。
```console.log("レンダリング")

このようにstateが更新されたときに関数コンポーネントは再び頭から処理が実行され、またstateが更新されたときに関数コンポーネントは再び頭から処理が実行され、またstateが更新されたらまた頭から...とぐるぐる回りながら差分のあるDOMを検知し、変更を反映して画面を表示している
この変更を検知してコンポーネントを再処理することを再レンダリングと呼ぶ
「おっstateが変更されてる、関数コンポーネント更新しよ」となるのが再レンダリングということね

### 副作用とuseEffect
reactHooksの機能の中のuseEffectについて。useStateのお友達
同じくreactからimportする
この子は「ある値が変わったときのみある処理を実行する」らしいけどそれってuseStateと変わんなくない？
第一引数にはアロー関数、第二引数には必ず配列で指定する。
stateと違ってマウント時にも実行されるから、コンポーネントを初回表示した時のみ実行みたく書くこともできるとか
あー、stateだと何度も再レンダリングして重くなるから変更した時だけでよくね？っていうときにEffectくんは役に立つのか
どう使い分けるのかな？回数少なければstateでも良さそ

## exportの種類
今まで使ってきたexportはノーマルexportというらしい
default exportと呼ばれるこいつは名前をつけることができる。それだけ。
１つのファイルに１回きりで正直あんまり使わない。普段もnormalを推奨。間違える恐れがあるため。
ノーマルexportでもas ~とすれば別名をつけられるみたいだし出番なくない？


## まとめ
JSXで書くときはreturn以降はタグを使え！
javascript書くときは[]を使う
関数でコンポーネントをつくって組み合わせて画面を作っていく
コンポーネントに渡すデータをprops(条件に応じて変わってくやつね)
コンポーネントが持つさまざまな状態をStateと呼ぶ
use StateとuseEffectの違いはある値が変わったときのみという部分
