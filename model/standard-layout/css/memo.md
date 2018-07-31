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

