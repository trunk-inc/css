# css
TRUNKで使用するcss

##　概要
BEMとGoogleのルールに則る
BEMは色々なルールがあるが、TRUNKは公式に則る

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


## <a href="#decimal_point">小数点の頭の「0」</a>
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


## <a href="#url_quote">URI値の引用符</a>
- url()での指定において、""（ダブルコーテーション）や''（シングルコーテーション）などのURI値の引用符を省略すること。

例)
```
NG
background-image: url("//www.google.com/css/go.css");

OK
background-image: url(//www.google.com/css/go.css);
```


***

## <a href="#HEX_color_code">HEX形式のカラーコード</a>
- HEX形式のカラーコードで3文字で表記できるものは3文字にする。
例)
```
<NG>
color: #eebbcc;

<OK>
color: #ebc;
```


***


## <a href="#prop_order">プロパティの記述順序</a>
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

## <a href="#block_indent">ブロック単位のインデント</a>
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


