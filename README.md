# TRUNK Css Style Guide

## 概要
- BEMとGoogleのルールに則る
- BEMは色々なルールがあるが、TRUNKは公式に則る

[BEM公式ドキュメント](https://en.bem.info/methodology/quick-start/#modifier) 
[google公式翻訳](http://buchineko.website/google_styleguide_html/)

参考
- [GoogleのCSSガイダンスに沿ったコーディング方法について](https://seopack.jp/internal-seo/basic/google-css-style-guide.php)
- [Google HTML/CSS Style Guide まとめ](https://qiita.com/Sugima/items/785644372397595644ba)

### BEMの書き方
- クラスは **ケバブケース** で書く
例) `.block-name` `.block-name__element_modifier`

- `block` は **小文字** 始まり 
例) `.block`
<br>

- `element` は **アンスコ2個**
例) `.block-name__element`
<br>

- `modifier` は **アンスコ1個**
例) `.block-name__element_modifier`
<br>

## 目次
 1. [ショートハンドプロパティ](#short_hand)
 1. [小数点の頭の「0」](#decimal_point)
 1. [URI値の引用符](#url_quote)
 1. [16進法のカラーコード](#HEX_color_code)
 1. [プロパティの記述順序](#prop_order)
 1. [ブロック単位のインデント](#block_indent)
 1. [プロパティ終端のセミコロン](#prop_last)
 1. [プロパティ終端のスペース](#prop_last_space)
 1. [セレクタ終端のスペース](#selector_last_space)
 1. [セレクタとプロパティの改行](#selector_prop_line)
 1. [タイプセレクタの指定方法](#type_selector)
 1. [コメントのルール](#comment)
 1. [Jsで扱う要素](#js_css)
 1. [font-size指定](#font_size)

<h2 id="validate">CSSバリデート</h2>
- 正確なcssなのか検証するため、[W3C CSS Validator](http://jigsaw.w3.org/css-validator/)でチェックする。

***

<h2 id="short_hand">ショートハンドプロパティ</h2>   

- 同じプロパティが複数ある場合はショートハンドを使う。
- 要注意なプロパティ `background`,`border`,`font`,`margin`,`padding`

例)
```
<NG>
padding-bottom: 2rem;
padding-left: 1rem;
padding-right: 1rem;
padding-top: 0;

<OK>
padding: 0 1rem 2rem;
```

***


<h2 id="#decimal_point">小数点の「0」を省略/単位の表記</h2>

- 小数点の頭の「0」は省略する。
- 値が0の場合は単位を省略する。

例)
```
/* 小数点を省略 */
<NG>
font-size: 0.8rem;
opacity: 0.5;
transition all 0.2s;

<OK>
font-size: .8rem;
opacity: .5;
transition all .2s;

/* 単位を省略 */
<NG>
margin: 0px;
padding: 0px;

<OK>
margin: 0;
padding: 0;
```


***

<h2 id="url_quote">URL値の引用符</h2>

- url()での指定において、""（ダブルコーテーション）や''（シングルコーテーション）などのURI値の引用符を省略すること。

例)
```
NG
background-image: url("//www.google.com/css/go.css");

OK
background-image: url(//www.google.com/css/go.css);
```


***

<h2 id="HEX_color_code">16進法カラーコード</h2>

- 16進法形式のカラーコードで3文字で表記できるものは3文字で。

例)

```
<NG>
color: #eebbcc;

<OK>
color: #ebc;
```


***

<h2 id="prop_order">プロパティ記述順序</h2>

- アルファベットの順に記述。ベンダープレフィックスは無視すること。ただし、例えば-moz接頭辞は-webkitの前に来る、などの順序は保つ。

例)

```
<NG>
width: 1059px;
border: 1px solid;
-moz-border-radius: 4px;
color: black;
text-align: center;
-webkit-border-radius: 4px;

<OK>
border: 1px solid;
-moz-border-radius: 4px;
-webkit-border-radius: 4px;
border-radius: 4px;
color: black;
text-align: center;
width: 1059px;
```


***

<h2 id="block_indent">ブロック単位のインデント</h2>

- 階層がわかりやすいように、ブロック単位でコードをインデントすること。

例)

```
<NG>
.block{
&__element{
color: #333;
display: block;
}
}

<OK>
.block{
  &__element{
   color: #333;
   display: block;
  }
}
```


***


<h2 id="prop_last">プロパティ終端のセミコロン</h2>

- すべてのプロパティの終端はセミコロンを書くこと。

例)

```
<NG>
.sample {
  display: block;
  height: 100px
}

<OK>
.sample {
  display: block;
  height: 100px;
}

```


***


<h2 id="prop_last_space">プロパティ名終端のスペース</h2>

- すべてのプロパティ名の終端のコロンの後にスペースを入れる。

例)

```
<NG>
.sample {
  display:block;
}

<OK>
.sample {
  display: block;
}

```


***

<h2 id="selector_last_space">セレクタ終端のスペース</h2>

- セレクタ終端に１つスペースを入れる。

例)

```
<NG>
#sample{
  margin-top: 1rem;
}

/* 改行は必要ない */
#sample
{
  margin-top: 1rem;
}

<OK>
#sample {
  margin-top: 1rem;
}

```

***


<h2 id="prop_last">プロパティの改行</h2>

- プロパティは改行して記述すること。

例)

```
<NG>
.sample {
  color: #444; display:block; width: 300px;
}

<OK>
.sample {
  color: #444;
  display: block;
  width: 300px;
}

```


***


<h2 id="selector_prop_line">セレクタとプロパティの改行</h2>

- 別々のセレクタとプロパティがある場合は改行して書くこと。

例)

```
<NG>
.sample, .hogehoge {
  display:block;
}

<OK>
.sample,
.hogehoge {
  display: block;
}

```


***


<h2 id="type_selector">タイプセレクタの指定方法</h2>

- 依存性をなくすため、タイプセレクタにIDとクラス名を記述しないようにする。子孫セレクタもできれば避ける。

例)

```
<NG>
ul#sample {
 hoge... 
}
div.sample {
 hoge...
}
  
<OK>
#sample {
 hoge...
}
.sample {
 hoge...
}
```

***


<h2 id="comment">コメントのルール</h2>

- セクション毎にコメントする
- コメントの形は`/* */`で囲む
- セクション終了時に `/* end */`と書く
- コメントを書く場合は上下1行あける

例)

```
<NG>
// header

// main

// footer

<OK>
/* header */

.header{
 hogehoge...
}

/* end */

/* main */

.main{
 hogehoge...
}

/* end */

/* footer */

.footer{
  hogehoge...
}

/* end */

複数行の場合は、
/*
hoge
hoge
*/
```


***


<h2 id="js_css">Jsで扱う要素</h2>

- jsでアニメーションをさせたり、jsで扱う部分は文頭に「js-」をつける
- 「js-」をつけていない要素はjsで扱わない。
- 「js-」のclassにstyleは記述しない。トリガーとしてだけ使う

例)

```

<NG>
/* styleを当てる */
.js-hoge{
 .......
}


<OK>
.js-hogehoge
#js-hogehoge
```


***


<h2 id="js_css">font-sizeの指定</h2>

- `rem`です。
- わかりやすい[記事](http://infinityforest.net/home/archives/3091)

例)

```
<OK>
.js-hogehoge
#js-hogehoge
```

***

## 外余白のルール
- 外に余白をつけるときは、matginをつける
- marginは原則に下方向`margin-bottom`をつける / 横方向は`margin-right`をつける

例)
```
<NG>
.sample {
  margin: 20px 0 0 20px;
  or
  margin-right: 20px;
}

<OK>
.sample {
  margin: 0 20px 20px 0;
  or
  margin-right: 20px;
}
```

## 擬似クラス
- 原則`last-child`を使う。
- 途中の要素を変更したい場合は`nth-of-type`と`nth-child`を使う
- `nth-oy-type`と`nth-child`の違いは要素（p, a, liなど）を判別して数えるかどうか。
[擬似クラス nth-childとnth-of-type](https://qiita.com/kudo_kk/items/8277c1f0eae18e15dd64)

例)
```
<NG>

 /* scss */
.sample {
  margin-right: 20px;
  &:first-child {
    margin-right: 0;
  }
}
  
<OK>
.sample {
  margin-right: 20px;
  &:last-child {
    margin-right: 0;
  }
}
```

## クラスの命名ルール

- 参考にしたもの[CSSのクラス名を決めるときに使うリストをつくりました](https://qiita.com/manabuyasuda/items/dbb76ed36970bec95470)

デザイン完成後

## SCSSのmixin

### メディアクエリ

例)

```
  <ブレイクポイント>
```
  @include mq-small {
    hogehoge
  }
```



