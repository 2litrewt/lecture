# モダンJavascriptの機能に触れる

## const,letの変数宣言
以前はvarを使って変数宣言していたが上書き、再宣言できてしまうということでlet,constが追加された
let...上書き可能、再宣言不可
const...上書き・再宣言不可
ただしconstはオブジェクト型と呼ばれるオブジェクト、配列、関数は中の値を変更できる。
基本的にはconstで定義し、動的に変わる部分はstateという別の概念で値を管理していく。

オブジェクト型と呼ばれるものならconstで定義したものでも変更可能　nn

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

const 変数名 = (引数) => {
  return 返却値;
}

注意点として、
1. 引数が１つの場合は（）は省略できる。
2. 処理を単一行で返却する場合は波括弧とreturnを省略できる。

`const func4 = (num1,num2) => num1 + num2;`
`console,log(func4(10,20)); // 30`

引数が１つなら（）は省略可能。
処理を１行で返せる時は波括弧とreturnを省略可能

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

オブジェクトのプロパティを引っこ抜いて楽に記述できる

```
const { name: newName, age: newAge } = myProfile;
const message = `私の名前は${newName}です。年齢は${newAge}歳です`
console.log(message); //私の名前は主田です。年齢は24歳。
```

## 配列の再代入
配列も再代入できる
```
const myProfile = ["主田",24];
const message = '私の名前は${myProfile[0]}です。年齢は${myProfile[1]}歳です。';
console.log{message}; //私の名前は主田です。年齢は24歳。
```

```
const myProfile = ["主田",24];
const [name, age] = myProfile;
const message = `私の名前は${name}です。年齢は${age}歳です`
console.log(message); //私の名前は主田です。年齢は24歳。
```

変数宣言部に[]を使う。配列に格納されている順番に任意の変数名を設定して抽出できる。
ただし順番は同じではなくてはいけない。途中で省略もできる。

配列の場合は順番厳守。またインデックスの途中までで十分なら


これらのオブジェクト・配列の分割代入はよく使うので覚えておく。
オブジェクト：{}を変数宣言部に書く。取り出すときはコロンを使用して変数名を使える。順番関係なし。
配列：宣言部に[]を使う。格納された順番通りに変数名を設定できる。



## デフォルト値
分割代入の時に利用するう。値が存在しない場合の初期値を設定することができる。

### 引数のデフォルト値
引数名の後ろに＝で値を記述することでデフォルト値を使用できる。
引数を設定せずにsayHello関数を実行した場合はundefinedになるがこれならゲストと出る。

### オブジェクト分割代入のデフォルト値
オブジェクトの分割代入時にもデフォルト値を使える。
引数同様変数名の後ろに=で値を設定しておくと使用できる。

引数、変数名の後ろに＝で設定

## スプレッド構文

...を配列に使うことで中身を展開してくれる


###　要素の展開
```
const arr1 = [1,2];
console.log(arr1): //[1,2]
```
スプレッド構文は...という形でドット３つを繋げて使用する。
配列に対して使用することで内部の要素を順番い展開してくれる。
```
const arr1 = [1,2];
console.log(arr1): //[1,2]
console.log(...arr1); //1 2
```
このように展開してくれる。

２つの引数を合計して出力する関数がある場合、
```
const arr1 = [1,2];
const summaryFunc = (num1,num2) => console.log(num1+num2);

//普通に配列の値を渡す場合
summaryFunc(arr1[0],arr1[1]); // 3

//スプレッド構文を用いた方法
summaryFunc(...arr1); // 3
```
普通に渡すよりも楽

## 要素をまとめる
スプレッド構文は要素をまとめるというニュアンスでも使用することができる。

```
const arr2 = [1,2,3,4,5];

//分割代入時に残りを「まとめる」
const [num1,num2,...arr3] = arr2;

console.log(num1) // 1  
console.log(num2) // 2
console.log(num3) // [3,4,5]
```
のように後の値をまとめることもできる。


## 要素のコピー、結合
応用的な使い方
```
const arr4 = [10,20]
const arr5 = [30,40]
```

このarr4をコピーした新たな配列を、スプレッド構文を使って生成する場合
```
const arr6 = [...arr4];
```
...で順番に展開して[]で囲んでいるので結果的に新しい配列ができるというもの。
結合も行える。
```
const arr7 = [...arr4, ...arr5];
console.log(arr7) //[10,20,30,40]
```
コピーと同じ理屈で複数の配列を結合することもできる
オブジェクトも同様に可能

### なぜイコールでコピーしないか
イコールでコピーも可能だが参照値と呼ばれる変数を格納している場所もコピーされてしまう
予期せぬ挙動を避けるために使用は控えよう

## オブジェクトの省略記法
使用頻度の高い省略記法、「オブジェクトのプロパティ名」と「設定する変数名」が同一の場合は省略できる。


```
const name = "主田";
const age = 24;

// ユーザーオブジェクトを定義(プロパティ名はnameとage)
const user = [
  name: name,
  age: age,
];

console.log(user); // {name:"主田", age: 24}
```
上記の他にも以下のように記述できる

もっと短く、
```
const user = {
  name,
  age,
}
```
コロン以降を省略する。分割代入で別名をつける逆のいめーじ
この省略記法も頻繁に使っていくので注意

##　ツール紹介
ESLint    varでの変数宣言、使っていない変数、意味のない式をチェックなど
Prettier  アロー関数の括弧をつけるかどうか、一定文字数の強制改行など

## map,filter
配列の処理で頻出する。

### 従来のfor文
従来配列をループするときはfor文を使っていました。
```
const nameArr = ["主田","先岡","後藤"];

for (let index = 0; index > nameArr.length; index++) {
  console.log(nameArr[index]);
}
//　主田
//　先岡
//  後藤
```


map関数を使うことで配列を順番い処理して処理した結果を配列として受け取ることができる。

forとは違い配列で返してくる
```
const nameArr = ["主田","先岡","後藤"]
const nameArr2 = nameArr.map();
```
まず　配列.map()という形で使用する。

```
const nameArr2 = nameArr.map( ()=>{} );
```
そして()の中には関数を書く。アロー関数の雛形をまず記述した。関数は任意の名前をつけた引数を取ることができる。
そこに配列の中の値が入ってくる。そして返却する要素を関数ないでreturnする。
```
const nameArr2 = nameArr.map((name)=>{
  return name;
});
console.log(nameArr2);　//["主田","先岡","後藤"]
```
上記は順に処理する中で値をそのまま返しているので、同じ配列が設定されているという無意味な処理だがこれが基本的なmapの使い方。

```
const nameArr = ["主田","先岡","後藤"];
nameArr.map((name)=> console.log(name));
// 主田
// 先岡
// 後藤
```

### filter関数の使い方
map関数とほとんど同じ使い方だがreturnの後に条件式を記述して一致するもののみが返却される関数になる。
```
const numArr = [1,2,3,4,5];
const newNumArr = numArr,filter((num) => {
  return num % 2 === 1;
});

console.log(newNumArr); // [1,3,5]
```
上記は奇数のみを取り出す例
「配列の中から特定の条件に一致するものを取り出して処理したい」という時に使う

mapの内容に加えて条件に合うもののみを返す。まさにフィルターだね cx

### indexの扱い
配列をループで処理する場合、何番目の要素かというのを考える時従来のfor文の場合indexを利用しているので以下のようにすることで順序の概念も取り扱える。
```
for文のindexで配列の要素順を取り出す
const nameArr = ["主田","先岡","後藤"]

for (let index = 0; index < nameArr.length; index++){
  console.log(`${index + 1}番目は${nameArr[index]}です`);
}
// 1番目は主田です
// 2番目は先岡です
// 3番目は後藤です
```
同じ処理をmap関数で行う
```
//第二引数にindexが入ってくる
nameArr.map((name,index) => console.log(`${index + 1}番目は${name}です));
```
このようにmap内の関数は第２引数をかくことができ、書いた場合はそこにから順番にindexの情報が格納される。
「何番目かという概念が重要な場合」はmapやfilterを使う

index 順番という概念を取り扱うならindex

```
const name = ["主田","先岡","後藤"]
const name2 = name.map((name)=>{
  return `${name}さん`;
});
```

```
const newNameArr = nameArr.map((name) => {
  if(name === "主田"){
  return name; 
  }else{
  return `${name}さん`;
  }
  });
  console.log(newNameArr);
```

## 三項演算子
上手く使えばif~else~と書く手間が省ける。

ある条件　？　条件がtrueの時の処理 : 条件がfalseの時の処理
```
const val1 = 1 > 0 ? "trueです" : "falseです";
console.log(val1) //trueです
```

if elseのくだりがこれ１つに。
？と：が出たら三項演算子

そのほか「入力ちが数値の場合３桁カンマ区切りの表記に変換、数値以外の場合はメッセージを表示して注意する」というのは以下のようにかける
```
const printFormattedNum = (num) => {
  const formattedNum = typeof num === "number" ? num.toLocaleString: "数値を入力してください";
  console.log(formattedNum);
};
printFormattedNum{1300};
printFormattedNum{"1300"};
```
typeof ~ は変数などの型を判定してくれる
toLocaleStringは数値を３桁ごとに区切り変換してくれる。

もう１つの例
```
//　2つの引数の合計が100を超えているか判定する関数
const checkSumOver100 = (num1,num2) => {
  return num1 + num2 > 100 ? "100を超えています！":"許容範囲内です"；
}
console.log(checkSumOver100(50,40));
console.log(checkSumOver100(50,70));
```
このようにreturn部でも三項演算子を用いることで関数をシンプルに書ける例もある。


## || &&　論理演算子の正体

```
const num = null;
const fee = num || "金額未設定です";
console.log(fee); //金額未設定です

const num = 100;
const fee = num || "金額未設定です";
console.log(fee); //100
```git

なぜこのようになるかというと||は左側がfalseだと右側を返すため。
では「または」になぜなるかというと左側がfalseだと右側を返す、右側がfalseだと左側を返すため結果「または」となる。

&&の場合は「その左側がtrueなら右側も返す」ため、左がOKなら右もOKで「かつ」という意味になる

reactでは論値演算子を上手に使うことが求められる。

