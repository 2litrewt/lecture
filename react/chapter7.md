#　グローバルなstate
propsを受け渡すのにすごい深い階層までバケツリレーのようにimportしてると先岡さんがブチ切れる。
そうならないためにもグローバルなstateを設定する。

## 必要な理由
例として作ったアプリではapp.jsx配下にcard.jsxとeditbutton.jsxがありcard.jsxはいちいちeditbuttonからimportしなければならない
これだと動作が遅くなるしメンテもし辛くなるぞ

## contextでのstate管理
色々管理するライブラリはある。reactの標準で搭載されているcontextを使う

### contextでグローバルstateの使い方
器を作る
providerを作りcontextの値を参照したいコンポーネント群を囲む
stateを参照したいコンポーネントでReact.useContextを使う

### ContextのState更新と参照
実際にやってみた
providerで共有したいとこを囲むらしい。原理はわからない

index.jsとapp.jsxの役割は？
省略記法ってなんだっけ

### 
１つのcontextオブジェクトで何かが更新されると、useContextでそのcontextを使っているものは全て更新される。
なので複数contextでなんやかんやしてたら全部更新されてしまう

## その他のグローバルstateを扱う方法
Context以外にもpropsを渡さずにstateを管理する方法がある
Redux・recoil
何が何やらさっぱり
