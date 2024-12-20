react 実践の教科書

# １.知っておきたいモダンjavascriptの基礎知識

## どこからがモダンjavascriptなのか
とくに決まりはないが以下のような特徴がある。
- react,vue,angularなどの仮想DOMを用いるライブラリやフレームワークを使用
- npm/yamなどのパッケージマネージャーを使用
- 主にES2015以降の記法を使用
- webpackなどのモジュールバンドラーを使用
- Babelなどのトランスパイラを使用
- SPAで作成　など

## DOM、仮想DOM
document object modelの略。
もともと要素を変更する際はDOMを直接操作して書き換えるような処理を行なっていた。
しかしこの方法では表示するのに時間がかかったり、コードが肥大化するという難点があった。
これらを解消するのが仮想DOM。javascriptのオブジェクトで作られた仮想的なDOMのことで、これを用いて実際のDOMとの差分を比較し変更箇所のみを実際のDOMni反映することでDOMの操作を最小限にできる。
reactはこれらの操作をいい感じにやってくれる。

一部だけ弄ってくれる仮想ドム

## パッケージマネージャー npm/yam
かつてのjsは１つのファイルに処理全てを書いていた。なのでとてつもない量になり管理が難しくなる。加えて再利用もできないのでとても効率が悪かった。
そこでJSファイルから他のJSファイルを読み込んで使えるように改善された。しかし読み込みじゅんを意識しないとエラーになるなど以前んとして問題はあった。
現在のjavascript開発ではnpm,yarnなどのパッケージマネージャーを使うことで解消している。

フロントエンド、バックエンド問わずさまざまなパケ0時を利用して開発は行われる。
そのパッケージのインストール、アップデートなどを担ってくれるのがパッケージマネージャー。
javascriptのnpm、rubyのgem,phpのcomposerなど

パッケージマネージャーの利点は以下の通り
- 依存関係を勝手に解消してくれる。
- チーム内でのパッケージの共有やバージョン統一が容易
- 世界中で公開されているパッケージをコマンド１つで利用可能
- どこから読み込んだものかわかりやすい

npmってとこから持ってくるからnpmってつけるのね

まず世界中の人がパッケージの公開場所として使用しているのがNPMというレジストリ。
（一般に大文字の場合はレジストリ、小文字の場合はパッケージマネージャーとしてのnpmを指すことが多い）
そして`npm install [パッケージ名]`,`yarn add [パッケージ名]`のコマンドでインストールする
上記コマンド時にローカルのpackage.json更新されパッケージ情報が追記される。
同時にnpmでインストールした場合package-lock.json、yamの場合はyarn.lockが生成される。
この２つを使うことで、パッケージとバージョンがわかるので他の人でも同様の環境が作れる
`npm install`,`yarn add`を実行することで作成できる。
実行するとnode_moduelsというフォルダが生成され、そこのパッケージが入る.
node_modulesはファイルサイズが大きくなるのでgithubにあげたりせずにpackageの２ファイルで再構築するように。
gitignoreにあげないファイル名を記述することで避けられる。

## ECMAScript
勝手にjsの内容変えないようにECMAという団体が管理してる。
javascriptは最初「Livescript」という名前だった。oracle社のjavaが人気があり影響を受けてjavascriptになった。
その後マイクロソフト社がJscriptという言語を開発したがjavascりptとは仕様が異なりややこしかった。
そこでECMAに標準化を依頼し出来上がったのがECMAscript。1年に１度更新がある。バージョンはESと呼ばれES6から西暦で呼ぶようになる。

## javascriptの転換期
ES2015でモダンjavascriptでも必須と言える文法や機能が加わった。
これらが今後の学習で触れていくものになる。
- let,constを用いた変数宣言
- アローファンクション
- Class構文
- 分割代入
- テンプレート文字列
- スプレッド構文
- Promise
etc...

## モジュールバンドラー、トランスパイラ

### モジュールバンドラー
複雑なプロジェクトでは設定ファイルをいじる必要が出てくるので概念を知っておくのは大切。
以下に解説。
分けて開発すると効率が良くなるが、本番環境では逆にパフォーマンス低下につながる。
「開発はファイルを分けて行い、本番用にビルドするときに１つのファイルにまとめよう」という思想を実現するためにjsファイルやcssファイルなどをまとめてくれるモジュールバンドラーが作られた。
これはファイルを１つにまとめる際に依存関係を解決してくれる優れもの。
あらかじめ設定ファイルを記述しておき、ビルドを実行するとモジュールバンドラーがいい感じにファイルをまとめてバンドル後のファイルを生成してくれる。そのファイルを本番環境に反映することでプログラムを実行することができる。webpackというのが主流。

パッケージマネージャ＞モジュールバンドラー・トランスパイラ＿

###　トランスパイラ
モジュールバンドラーが複数のファイルに１つにまとめてもらえるものだとしたら、トランスパイラはjavascriptの記法をブラウザで実行できる形に変換してくれるもの。
ECMscriptが更新されるてもブラウザが対応していないことはよくある。ES2015ではIE11が全く動かないなども。
そこでトランスパイラを利用すると新しい記法を古い記法に変換してくれる。reactだとjsファイルにJSX記法という特殊なルールの書き方で記述していくのですが、そういったものもブラウザが認識できる形に自動で変換してくれる。
Babelと呼ばれるトランスパイラが主流。



##　まとめ
いずれも効率よく開発、実行は上手に変換ができること。
この辺りは最近のフレームワークやライブラリ側が隠しているので気づくことは少ないかも。

## SPAと従来の表示の仕組み
ここは何度もやったところ、HTMLのリクエストをした後更新に必要なデータのみをもらいブラウザ上で更新する。

開発者にもメリットがあり、コンポーネントと呼ばれる各要素を定義したものを設定できるので、１部分の編集でページ全体のデザインの変更が可能。