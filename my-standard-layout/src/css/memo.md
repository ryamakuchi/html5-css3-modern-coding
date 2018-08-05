# Chapter-02

## floatとclearfix
* floatを使用すると、親の高さが0になる
（親がfloatをかけた子の高さを認識できなくなるため）

それを回避するために　以下のコードをpartsに追加する
```
.clearfix::after {
  content: '';
  display: block;
  clear: both; // 回り込みを解除するプロパティ
}
```


## box-sizing
* ボックスモデルは、外側から
    * margin
    * border
    * padding
    * content

* widthとheightをどこまで含めるかを変えるプロパティ

* box-sizing: content-box; // 初期値
    * paddingとborderを幅と高さに含めない

* box-sizing: border-box;
    * paddingとborderを幅と高さに含める

* box-sizing: inherit;
    * 親要素のborder-boxの値を引き継ぐ

```
*, *::before, *::after {
  box-sizing: border-box; // paddingまで含めると計算しやすい
}
```



# Chapter-03

## background
* backgroundは要素の背景に関わるプロパティをまとめて指定できるショートハンドプロパティ

* 初期値
```
background-color: transparent
background-image: none
background-repeat: repeat
background-position: 0% 0%
background-size: auto auto
background-attachment: scroll →背景画像のスクロールの有無
```
* background-sizeはbackground-potisionの後にスラッシュ区切りで続けて書く必要がある

`background: left 5% / 15% 60% repeat-x url("../../media/examples/star.png");`

## box-shadow
```
box-shadow: [右方向のずれ] [下方向のずれ] [ぼかしの大きさ] [拡張の大きさ] [影の色];
```
* カンマで区切ることで複数の影を指定することができる

⚠︎ 新しいプロパティで影をつける選択肢もある
https://ferret-plus.com/8961


## marginの相殺
* 上下のmarginは相殺されてしまうため、上の余白をとるときはpaddingをとることが好ましい


## border-radius
* 指定方法はmargin,paddingと同じく、左上が起点の時計まわり
* / を入れて指定すると、x / y の概念になる
* % を入れて指定する場合は、widthとheightを指定する
* border-x-y-radiusプロパティで個別に指定することもできる


## transition
* transitionはトランジションに関わるショートハンドプロパティ
* 初期値
```
transition-property: all →トランジションを適用するプロパティを指定
transition-duration: 0s →値が変更するまでの時間
transition-timing-function: ease →変化の仕方の種類
transition-delay: 0s →変化が始まるまでの時間
```
* durationとdelayは両方時間なので、delayを指定するときは必ずdurationも指定すること

⚠︎ transitionはIE10~対応



# Chapter-04

## display
* blockは、divのような挙動。要素をブロック化することができる
* inline-blockは、文章の中で使えるブロックのように、並べたりできるブロック要素
* inlineは、文章のような要素。widthやheightを指定できない

⚠︎ まだまだよくわかっていないことあり、調べておくこと


## opacityと-webkit-font-smoothing
### opacityにtransitionをかけた時に、Safariでチラつく問題があるらしい…
* 自分で確かめてないので分からないけれど
```
body {
    -webkit-font-smoothing: antiailiased;
}
```
を入れると、チラつき防止になるらしい！

⚠︎ まだ草案なので、ベンダープレフィックスつけること

参考：

https://caniuse.com/#search=font-smoothing
https://qiita.com/hata-mu/items/98df93516cbd3f1cc418


## HTMLのtime要素
* time要素にはdatetimeという属性をつけることができる
* テキストの表示形式に左右されない、正確な日時を機械に対して伝えることができる

```
datetime="2018-08-03T22:48"
```
* 時刻まで含めるときは、間にTをはさむ

