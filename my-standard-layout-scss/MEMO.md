# Chapter-02

## floatとclearfix
* floatを使用すると、親の高さが0になる
(親がfloatをかけた子の高さを認識できなくなるため)

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


## line-height
* 行間を指定できる
    * normal(初期値)
    * 数値 + 単位(px,rem)
    * 割合(%) ... 要素のfont-sizeを基準とした割合
    * 数値のみ ... 要素のfont-sizeにこの値をかけた数値
* 数値のみの指定法がよく使われる！
子要素にもline-heightは引き継がれるため、
絶対基準ではなく相対基準で書いたほうがよいため


## overflow
* 要素からはみ出したコンテンツの表示方法を指定できる
    * visible(初期値)
    * hidden
    * scroll ... スクロールバーは常に表示される
    * auto ... ブラウザに依存する(スクロール領域があればスクロールが表示される)


## width min-width max-width
* 最小幅と最低幅が指定できる


## nth-typeとnth-child擬似クラス
* nth-type(n)で「同じ階層のn番目の要素」にスタイルを当てることができる
* nに指定できるのは整数、数式、even(偶数)、odd(奇数)
* 数えられるのは、その要素の子要素のため、クラス指定しても常に要素ごとの順番が数えられる


## text-overflow: ellipsis;
* 表示領域からはみ出て見えなくなる時のテキストの最後に...をつけてくれる
    * clip(初期値) ... 表示領域を境目にして非表示になる
    * ellipsis ... テキストの最後は...で表示される
* 通常は折り返して表示されてしまうので、一緒に
white-space: nowrap;も指定する
```
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
```


# Chapter-05

## vertical-align
* 要素の縦方向の配置の基準を指定できる
    * baseline(初期値) ... 英語の底の位置
    * middle ... 対象要素の中央のライン
    * text-top ... 対象要素の文字の最上部ライン
    * text-bottom ... 対象要素の文字の最下部ライン
    * top ... 対象要素の行の最上部ライン
    * bottom ... 対象要素の行の最下部ライン
    * 数値+単位 ... 対象要素のベースラインを、
    親要素のベースラインから指定の割合分距離を置いた位置にそろえる
    * % ... 対象要素のline-heightの高さを100%として、
    対象要素のベースラインを親要素のベースラインから指定の割合分距離を置いた位置にそろえる

## transform
* 要素を移動、回転、変形することができる
* scale(x, y) ... (拡大､縮小)数値のみで単位はいらない
* skewX(30deg), skewY(30deg) ... (傾斜)
* translate(x, y) ... (移動)
* rotate(45deg) ... 回転

## transform-origin
* 変形するときの基準になる点を決めるプロパティ
* transform-origin: x, y;

## CSSカウンタ
* CSSの中でカウンタを定義して値を増やしたり表示したりすることができる
    1. カウンタの名前を決める
    2. カウンタの値を0に初期化する ... (counter-reset: カウンタ名)
    3. カウンタの値を表示する ... (content: counter(カウンタ名))
    4. カウンタの値を増加させる ... (counter-increment: カウンタ名)

## セレクタについて
* A B … 子孫セレクタ(A以下にあるB)
* A > B … 小セレクタ(A直下にあるB)
* A + B … 隣接セレクタ(Aの直後にあるB)
* A ~ B … 関節セレクタ(Aと同改装でA以降にあるB)

## cursor
* マウスポインタの形を指定できる
* 色々指定できたり、画像に変えたりもできる


# Chapter-06

## border-styleに指定できる線の種類
* none ... (初期値)
* hidden ... (非表示)
* dashed ... (破線)
* dotted ... (点線)
* inset ... (彫り込んだボックス)
* outset ... (浮き出たボックス)
* groove ... (彫り込んだ線)
* ridge ... (浮き出た線)
    * noneとhiddenは同じく非表示だが、他の線と重なったとき、
        * noneは他の線が優先される
        * hiddenはhiddenの線が優先される

