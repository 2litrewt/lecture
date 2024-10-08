# モダンJavascriptの機能に触れる

## const,letの変数宣言
以前はvarを使って変数宣言していたが上書き、再宣言できてしまうということでlet,constが追加された
let...上書き可能、再宣言不可
const...上書き・再宣言不可
ただしconstはオブジェクト型と呼ばれるオブジェクト、配列、関数は中の値を変更できる。
基本的にはconstで定義し、動的に変わる部分はstateという別の概念で値を管理していく。

## テンプレート文字列
文字列の中で変数を展開するもの。rubyの式展開みたいなもの。
バッククウォートと＄と{}を利用。

## アロー関数（）　=> {}
アロー関数はシンプルに関数を記述できる。

従来の関数はfunctionという記述の後に関数名や引数、処理内容を記述していました。
また宣言した関数を変数に一度格納してから実行するなども（よくこれやってた）

アロー関数はfunctionは使わず,
```
const func2 = (value) => {
  return value;
}
```
で定義する。

注意点として、
1. 引数が１つの場合は（）は省略できる。
2. 処理を単一行で返却する場合は波括弧とreturnを省略できる。

`const func4 = (num1,num2) => num1 + num2;`
`console,log(func4(10,20)); // 30`

また返却値が複数業に及ぶ場合は（）を使うことで単一行のようにまとめて返却することができる

```
const func5 = (num1,num2) => (
  {
  name:num1 
  age:num2
  }
)
```

`console,log(func5("主田",24)); // {name: "主田", age: 24}`

## 分割代入
オブジェクトや配列から値を抽出するための方法

- 用いない場合
```
const myProfile = {
  name: "主田",
  age: "24",
};

const message = `私の名前は${myProfile.name}です。年齢は${myProfile.age}歳です。`;

console.log(message); //私の名前は主田です。年齢は24歳。
```

- 用いる場合
```
const { name,age } = myProfile;
const message = `私の名前は${name}です。年齢は${age}歳です`
console.log(message); //私の名前は主田です。年齢は24歳。
```
{}を変数宣言部に使用することでオブジェクト内から一致するプロパティを取り出すことができる。
また取り出したものに：(コロン)を使用することでその変数名を使うこともできる

```
const { name: newName, age: newAge } = myProfile;
const message = `私の名前は${newName}です。年齢は${newAge}歳です`
console.log(message); //私の名前は主田です。年齢は24歳。
```

## 配列の再代入
配列も再代入できる
```
const myProfile = ["主田",24];
const message = '私の名前は${[]}です。年齢は${myProfile[]}歳です。';
console.log{message}; //私の名前は主田です。年齢は24歳。
```

```
const myProfile = ["主田",24];
const [name, age] = myProfile;
const message = `私の名前は${name}です。年齢は${age}歳です`
console.log(message); //私の名前は主田です。年齢は24歳。
```

変数宣言部に