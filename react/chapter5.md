# ReactとCSS

CSSの当て方にも色々あってこれが主流というのはないらしい。
何種類かあるので解説。

## Inline Styles
一般的なCSSの記述方。
よく見るjavascriptのオブジェクトの形で記述し、タグのStyleで設定する。
`<div style={{width:"100%", padding:"16px"}}>`

注意点として、
- プロパティ名はキャメルケースで書く
- 値は文字列か数値のみ（逆に他のって何があるんだ？）
- 煩雑になるから使いすぎない。reactではマイナーってわけ？

## CSS Modules
従来のweb開発でよくある（そうなの？）.cssや.scssファイルを定義していくやり方。
ほかと異なるのがコンポーネントごとにCSSファイルを用意することが多い。なんで？
試してみたらcssファイルからimportして使うみたい。上のインラインスタイル
と違ってファイルが別だから読みやすいし描きやすい

## styled JSX
Next.jsに標準で組み込まれている
CSS-in-JSと呼ばれるコンポーネントに記述していく
別にタグを挟んで使用する。hoverとかSCSS記法は使えないから、このCSSを使うときは前述のNext.jsの時にとりあえず使うかーという感じ

## styled components
人気のライブラリで、スタイルを当てたコンポーネントを定義するという特徴
STyledJsxと同じCSS-in-JSというやつ
classNameに定義するのではなく独自でタグを定義する
styledComponentsと違ってSCSSが使える

## Emotion
上と同じくらい人気のやつ。
inlineStyles,StyledJSX,StyledComponentsと似た書き方が用意されている万能選手。
とりあえずどんな書き方がいいか模索するとにちょうどいい

## tailwind
tailwiindが用意したのをclassnameで書く。
変更箇所を全部書くので長くなるが、その一文だけで完結している
クラス名やコンポーネントの名前が決まっているので名前付けについて考えなくていいというのも特徴
