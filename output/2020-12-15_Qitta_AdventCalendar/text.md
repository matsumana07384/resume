
HTMLのInput要素のinputmodeのスマートフォンのキーボードがどのように表示されるを整理してみた


# はじめに
この記事は[ZOZOテクノロジーズ #4 Advent Calendar 2020](https://qiita.com/advent-calendar/2020/zozo_tech4) の15日目の記事です。
昨日は [@TAKAyuki_atkwsk](https://qiita.com/TAKAyuki_atkwsk)さんの[ALB で gRPC を利用する on EKS - Blogaomu](https://www.blogaomu.com/entry/alb-grpc-on-eks)でした。

## 概要
タイトルの通り、HTMLのInput要素のinputmodeのスマートフォンのキーボードがどのように表示されるかを整理してみた記事です。  
調査としている方の参考になればと思い、記事にしました。  

### 書いてあること
- inputmodeのざっくり説明
- サンプルコード
- inputmodeで表示されるiOSとAndrodiのキーボード表示

### 書いていないこと
- inputmodeの詳細な説明
- 想定しているキーボードを表示させるための工夫

# 内容

## inputmodeとは？
その名の通り、input要素の入力時に表示されるソフトウェアキーボードの種類を指定する属性。  
HTML5.2で一度廃止[^1]されたものの、Living Standard[^2]にて復活しています。  


## 検証端末
- iOS
  - iPhone SE 2nd generation（Simulator）
  - iOS 14.2
  - Safari
  - 標準キーボード（第一言語：日本語）

- Android
  - Galaxy S10
  - Android 10.0
  - Chrome
  - [Gboard](https://play.google.com/store/apps/details?id=com.google.android.inputmethod.latin&hl=en_US&gl=US)

## 調査結果一覧

### none
``` HTML
<input inputmode="none">
```

**説明**
- キーボードが表示されない
- ページで独自にキーボードを実装している場合などに用いられる

**表示**

| iOS | Andoroid  |
|---|---|
| なし  |  なし  |


### text
``` HTML
<input inputmode="text">
```

**説明**
-  標準のキーボードが表示
- `Inputmode` の指定がない場合は、このキーボードが表示される

**表示**
| iOS | Andoroid  |
|---|---|
|  <img src="https://github.com/matsumana07384/memorandum/blob/master/output/2020-12-15_Qitta_AdventCalendar/img/iOS_text.png?raw=true" width="375" height="auto">  |   <img src="https://github.com/matsumana07384/memorandum/blob/master/output/2020-12-15_Qitta_AdventCalendar/img/Android_text.jpg?raw=true" width="375" height="auto">  |


### tel
``` HTML
<input inputmode="tel">
```

**説明**
- 電話番号の入力に最適化されたキーボードが表示
- 0 から 9 までの数字とアスタリスク ( `* ` )、シャープ ( `#` ) キーなどが表示される
- 電話番号を入力するフォームの場合は、`<input type="tel">` が推奨される
 
**表示**

| iOS | Andoroid  |
|---|---|
|  <img src="https://github.com/matsumana07384/memorandum/blob/master/output/2020-12-15_Qitta_AdventCalendar/img/iOS_tel.png?raw=true" width="375" height="auto">  |   <img src="https://github.com/matsumana07384/memorandum/blob/master/output/2020-12-15_Qitta_AdventCalendar/img/Android_tel.jpg?raw=true" width="375" height="auto">  |


### url
``` HTML
<input inputmode="url">
```

**説明**
- URLの入力に最適化されたキーボードが表示
- スラッシュ（ `/` ）が入力しやすい位置に配置されている
- URLを入力するフォーム場合は、 `<input type="url">`  が推奨される

**表示**

| iOS | Andoroid  |
|---|---|
|  <img src="https://github.com/matsumana07384/memorandum/blob/master/output/2020-12-15_Qitta_AdventCalendar/img/iOS_url.png?raw=true" width="375" height="auto">  |   <img src="https://github.com/matsumana07384/memorandum/blob/master/output/2020-12-15_Qitta_AdventCalendar/img/Android_url.jpg?raw=true" width="375" height="auto">  |

※Andoridの方の入力言語を日本語（あ）から英語（a）に変更すると、「/」が表示されます


### email
``` HTML
<input inputmode="email">
```

**説明**
- メールアドレスの入力に最適化されたキーボードが表示
- アットマーク（ `@` ）が入力しやすい位置に配置されている
- メールアドレスを入力するフォームの場合は、<input type="email"> を推奨

**表示**

| iOS | Andoroid  |
|---|---|
|  <img src="https://github.com/matsumana07384/memorandum/blob/master/output/2020-12-15_Qitta_AdventCalendar/img/iOS_email.png?raw=true" width="375" height="auto">  |   <img src="https://github.com/matsumana07384/memorandum/blob/master/output/2020-12-15_Qitta_AdventCalendar/img/Android_email.jpg?raw=true" width="375" height="auto">  |

※iOSの方の入力言語を日本語から英語（ABC）に変更すると「@」が表示されます

### numeric
``` HTML
<input inputmode="numeric">
```

**説明**
- 数字の入力ができるキーボードが表示
- 端末によっては負号（ `-` ）が入力できる

**表示**

| iOS | Andoroid  |
|---|---|
|  <img src="https://github.com/matsumana07384/memorandum/blob/master/output/2020-12-15_Qitta_AdventCalendar/img/iOS_numeric.png?raw=true" width="375" height="auto">  |   <img src="https://github.com/matsumana07384/memorandum/blob/master/output/2020-12-15_Qitta_AdventCalendar/img/Android_numeric.jpg?raw=true" width="375" height="auto">  |


### decimal
``` HTML
<input inputmode="decimal">
```

**説明**
- 実数と区切り文字（ピリオド（.） またはカンマ （,））が入力できるキーボードが表示
- 端末によっては負号（-）が入力できる

**表示**

| iOS | Andoroid  |
|---|---|
|  <img src="https://github.com/matsumana07384/memorandum/blob/master/output/2020-12-15_Qitta_AdventCalendar/img/iOS_numeric.png?raw=true" width="375" height="auto">  |   <img src="https://github.com/matsumana07384/memorandum/blob/master/output/2020-12-15_Qitta_AdventCalendar/img/Android_numeric.jpg?raw=true" width="375" height="auto">  |


### search
``` HTML
<input inputmode="search">
```

**説明**
- 検索の入力に最適化されたキーボードが表示
- return/submitキーの箇所が「検索」になっている
- 検索内容を入力するフォームの場合は、`<input type="search">`  を推奨

**表示**

| iOS | Andoroid  |
|---|---|
|  <img src="https://github.com/matsumana07384/memorandum/blob/master/output/2020-12-15_Qitta_AdventCalendar/img/iOS_search.png?raw=true" width="375" height="auto">  |   <img src="https://github.com/matsumana07384/memorandum/blob/master/output/2020-12-15_Qitta_AdventCalendar/img/Android_search.jpg?raw=true" width="375" height="auto">  |


# おわりに
いかがでしたでしょうか？
`inputmode` を指定しても想定通りのキーボードが表示されないケースがあることがわかってしまいました。

キーボード表示を指定できる他のやり方としては `type` を指定する方法もあります。
こちらも同じくキーボードの入力言語によって表示が異なるケースが出てくるため、開発者が考える最適なキーボードをどのパターンでも表示させることはまだまだ難しいな、という印象です。
  
完璧に！というよりはちょっと入力の補助できたらいいよね、ぐらいのゆるいスタンスで使っていくとよさそうだなと個人的には思います。


明日は [@akitok](https://qiita.com/akitok) さんの記事になります。
明日もお楽しみに😁！

## 参考記事
[<input>: 入力欄 (フォーム入力) 要素 - HTML: HyperText Markup Language | MDN](https://developer.mozilla.org/ja/docs/Web/HTML/Element/input)
[HTML Living standard｜HTML5｜HTML－havin' a coffee break｜珈琲とウェブデザイン](https://web.havincoffee.com/html/html5/html5_a_ls.html#inpage-ank11) 

[^1][HTML 5.2: Changes](https://www.w3.org/TR/html52/changes.html#features-removed)
[^2][HTML Standard](https://html.spec.whatwg.org/multipage/)

