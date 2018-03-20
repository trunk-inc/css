# TRUNK Css Style Guide

## 概要
- BEMとGoogleのルールに則る
- BEMは色々なルールがあるが、TRUNKは公式に則る

[BEM公式ドキュメント](https://en.bem.info/methodology/quick-start/#modifier) 
[google公式翻訳](http://buchineko.website/google_styleguide_html/)

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

## index
 1. [ショートハンドプロパティ](#short_hand)
 1. [小数点の頭の「0」](#decimal_point)
 1. [URI値の引用符](#url_quote)
 1. [HEX形式のカラーコード](#HEX_color_code)
 1. [プロパティの記述順序](#prop_order)
 1. [ブロック単位のインデント](#block_indent)
 1. [プロパティ最後のセミコロン](#prop_last)
 1. [プロパティ名最後のスペース](#prop_last_space)
 1. [セレクタとプロパティの改行](#selector_prop_line)
  
<h2 id="short_hand">ショートハンドプロパティ</h2>   
- 同じプロパティが複数ある場合はショートハンドを使う。

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


<h2 id="#decimal_point">小数点の「0」を省略</h2>
- 小数点の頭の「0」は省略する。

例)
```
<NG>
font-size: 0.8rem;
opacity: 0.5;
transition all 0.2s;

<OK>
font-size: .8rem;
opacity: .5;
transition all .2s;
```


***

<h2 id="url_quote">URI値の引用符</h2>  
- url()での指定において、""（ダブルコーテーション）や''（シングルコーテーション）などのURI値の引用符を省略すること。

例)
```
NG
background-image: url("//www.google.com/css/go.css");

OK
background-image: url(//www.google.com/css/go.css);
```


***

<h2 id="HEX_color_code">HEXカラーコード</h2>
- HEX形式のカラーコードで3文字で表記できるものは3文字で。
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


<h2 id="prop_last">プロパティ最後のセミコロン</h2>
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


<h2 id="prop_last_space">プロパティ名最後のスペース</h2>
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

例)

```
<NG>
// hogehoge

<OK>
/* hogehoge */

複数行の場合は、
/*
hoge
hoge
*/
```


***
