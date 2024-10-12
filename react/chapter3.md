# DOM操作

まずは普通にDOM操作すルトどのくらいめんどくさいかやる
getElementByIdやquerySelector、getElementByClassNameでとる
getElementByClassNameではHTMLCollection、querySelectorAllではNodeListが取得できる。
上記のように従来の開発では「何に」対して何を行うかというのを明確にする必要があった。
idやclass,タグ名、階層構造を駆使して操作対象DOMを取得するのが手間でバグが起きやすいなどもあった

## DOMの作成、追加、削除

### DOMの作成
javascriptの機能を用いることでこれまで取得してきたようなElementsをcreateElementde()作成することができる
引数にHTMLタグ名を入れることで作成する。

### DOMの追加
作成したElementnに対して要素を追加することもできる
appendChildを使うことで子要素として追加する。
前に追加したい場合はprependを使う。

コンソールで上記操作を行うことでその場でブラウザ上にボタンなどを追加できる

### DOMの削除
removeChildで行える。
その配下から指定されたElementowo除去することができる。
子要素全て削除したいときはtextContentに対してnullを設定してあげるといい。

## JavaScriptによるDOM操作の実践
