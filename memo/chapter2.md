# JS の読み込み

`<script>`の設置場所は以下の 3 つがある。

- `<body>`タグの配下
  - 実行結果を文書内に埋め込みたい時
- `<body>`タグの配下・`</body>`の前
  - ページを操作するコードを記述する場合
- `<head>`要素の配下
  - `<body>`配下で直接呼び出す前に定義しておく場合

`<script>`は外部呼び出しも可能。外部ファイルの読み込みは以下のように行う。

```html
<script src="ファイル名.js"></script>
```

コードを外部化することで、次のようなメリットがある。

- .html ファイルがすっきりする
- コードが再利用しやすい

ちなみに、以下の場合、`<script>`内のコードは実行されない。

```html
<script src="ファイル名.js">
  console.log("このコードは実行されない");
</script>
```

また、JS が実行されない環境では、`<noscript>`タグ内のコードが実行される。

```html
<noscript>
  <p>JavaScriptが無効になっています</p>
</noscript>
```

## JavaScript のルール

JavaScript には、以下のようなルールがある。

- 文の末尾はセミコロンで終わる
- 文の途中で、空白・改行・タブを入れても問題ない
  - ただし、コードの可読性を考え、適切にインデントを入れることが望ましい
- 大文字と小文字は区別される

## コメント

コメントの記法は以下の通り。

原則として、コメントは１行コメントを使う。複数行コメントは、特定の箇所を一時的に無効にする際に使用する。

```js
// 1行コメント

/*
複数行コメント
*/
```

Q.コメントには何を書くべきか？ A.コードの意図や処理内容を記述する。コードの内容がわかりにくい場合、コメントを書くことで他の人が理解しやすくなる。

具体的には、以下のような内容をコメントに記述する。

- 複雑なコードの意図
- クラスや関数、コードの説明
- 例えば、TODO / FIXME / OPTIMIZE / REVIEW などの記述
- コードの翻訳は記述しない

---

## 変数

### 変数の宣言

```js
let 変数名 = 値;
```

[注意点: 変数の宣言での「しないほうが良い」こと]

1. 初期値のない変数宣言
2. 複数の宣言を１行で行う
3. `var`による変数宣言
4. 変数宣言の省略

### 変数の命名規則

以下のルールに沿った命名を行う。

1. Unicode 文字・ドル文字・アンダースコア・数字から構成すること
2. １文字目は数字以外であること
3. 大文字/小文字は区別されること
4. 予約後ではないこと

[?]予約語とは？

予約ごとは、JavaScript が事前に定義しているキーワードのこと。予約語を変数名に使うと、エラーが発生する。

例）`if`, `break`, `do`, `void`, `while`, `with` など

また、string や number などのグローバルオブジェクトも避けるべき。

また、より読みやすいコードを目指すために、以下のような命名規則を守る。

1. 名前から役割が推測できること
2. 良い感じの長さにすること
3. 見た目がわずらわしくないこと
4. １文字目の\_はなるべく避けること
5. ローマ字の命名を避けること

なお、一般的には

- 変数名はキャメルケース（camelCase）で記述することが多い。
- 定数はスネークケース（SNAKECASE, snake_case）で記述することが多い。
- クラス名はパスカルケース（PascalCase）で記述することが多い。

## 定数の宣言

定数は、`const`を使って宣言する。

定数名は、大文字で記述することが多い。

```js
const 定数名 = 値;
```

## データ型

| データ型          | 概要                                                   |
| ----------------- | ------------------------------------------------------ |
| number（数値）    | 数値を扱う（制限あり）                                 |
| bigint            | number 以上の数値を扱う                                |
| string（文字列）  | クォートで囲まれた０個以上の文字列を扱う               |
| boolean（真偽値） | true または false の値を扱う                           |
| symbol            | 唯一の識別子を生成する                                 |
| null/undefined    | 何もないことを示す                                     |
| array             | データの集合を扱う（アクセスには、インデックスを使う） |
| object            | キーと値のペアを扱う（アクセスには、キーを使う）       |
| function          | 関数を扱う                                             |

### 真偽値(boolean)

Javascript では、以下のような値を「falsy」として扱う。

- 空文字列
- 0
- null
- undefined
- NaN
- false

### 数値(number)

数値リテラつは、「整数リテラル」と「浮動小数点リテラル」の２つがある。

- 整数リテラル
  - 10 進数: 0-9
  - 16 進数: 0x で始まる
  - 8 進数: 0 で始まる
  - 2 進数: 0b で始まる
- 浮動小数点リテラル
  - 小数点を含む数値
  - <仮数部>e<指数部> で指数表記も可能 例）1.23e4
  - 本来の値の計算は、「<仮数部> \* 10^<指数部>」となる

なお、ES2021 から、数値リテラルの区切り文字として、アンダースコア（\_）が使えるようになった。

数値セパレータは、あくまで見た目の整理のためのもので、数値の値には影響しない。

```js
// 例）1,000,000
const num = 1_000_000;
```

## 文字列(string)

文字列をシングルクォート（'）またはダブルクォート（"）で囲む。

```js
const str = "文字列";
```

文字列には、エスケープシーケンスを使うことができる。

代表的なエスケープシーケンスは以下の通り。

| エスケープシーケンス | 意味               |
| -------------------- | ------------------ |
| \n                   | 改行               |
| \t                   | タブ               |
| \r                   | キャリッジリターン |
| \'                   | シングルクォート   |
| \"                   | ダブルクォート     |
| \\                   | バックスラッシュ   |

テンプレート文字列を使うことで、文字列の中に変数を埋め込むことができる。

```js
const name = "太郎";
const str = `こんにちは、${name}さん`;
```

## 配列(array)

配列は、複数のデータを格納するためのオブジェクト。

なお、配列内の ',' は省略可能。

```js
// 配列の宣言
const arr = [1, 2, 3];
// 配列の要素へのアクセス
console.log(arr[0]); // 1
// 配列の要素の変更
arr[0] = 4;
console.log(arr); // [4, 2, 3]
// 配列の要素の追加
arr.push(5); // [4, 2, 3, 5]
arr[7] = 6; // [4, 2, 3, 5, <3 empty items>, 6]

//入れ子の配列
//配列の要素に配列を入れることも可能
//その長さは、バラバラでも良い（ジャグ配列）
const arr2 = [
  [1, 2],
  [3, 4, 5],
  [6, 7],
];
```

## オブジェクト(object)

オブジェクトは、キーと値のペアを格納するためのオブジェクト。

```js
// オブジェクトの宣言
const obj = {
  key1: "value1",
  key2: "value2",
  key3: [1, 2, 3],
};
// オブジェクトの要素へのアクセス
// 1. ドット記法
console.log(obj.key1); // value1
// 2. ブラケット記法
console.log(obj["key1"]); // value1

// オブジェクトの要素の変更
obj.key1 = "value3";
console.log(obj); // { key1: "value3", key2: "value2" }
// オブジェクトの要素の追加
obj.key4 = "value4";
```

## 関数(function)

関数とは、何かしらの入力値を受け取り、処理を行い、その結果（戻り値）を返すもの。

### 未定義値(undefined)とヌル値(null)

### 未定義値(undefined)

- 宣言済みの変数だが、値が代入されていない状態
- 未定義のプロパティにアクセスした場合
- 関数の戻り値がない場合

### ヌル値(null)

nullは、何もないことを示す特殊な値。
