# TRUNK Css Style Guide

## 概要
- react componentとの親和性を考慮し、chainable bemを採用する
- 下記の参考に加え、javascriptのクラス命名の慣例に沿ってルールを加える
- react componentと対になるようにファイルを作成する
- BEMなので基本ネストは使用しない。（エディタでの検索効率も上がる）
- `js-` プレフィックスはreactの際は基本使用しない

### css(scss)のディレクトリ構成
```
/(cssのルート)
  atoms
    _button.scss
    _index.scss <= atomsを全てインポート
  molecules
  organisms
  templates
  pages
  layouts
  variables <= 変数を格納
    _color.scss
    _index_.scss
  mixins <= mixinを格納
    _mediaquery.scss
    _index.scss
  application.scss
```

参考
- [Chainable BEM modifiers](https://webuild.envato.com/blog/chainable-bem-modifiers/)

### cahinable bemの書き方
- クラスは **アッパーキャメル** で書く
  - javascriptのクラス名に合わせる為にアッパーキャメルは独自ルール
  - `modifire` はクラスではないのでキャメルケース
```
.Block {}
.Block__Element {}
```

- `element` は **アンスコ2個**  
```
.BlockName__Element
```

- `modifier` は **別クラスを定義し、ハイフンをプレフィックスとしてつける**  
```
.BlockName__Element {}
.BlockName__Element.-large {}
```

## 制作フロー

### Prを出すまでの流れ(作業者)

1. ガイドラインに沿ってコーディングする
2. 作業後必ず`sass-lint`を通す
3. `守ってほしいルール`を守れているのか確認する
4. 通ればPrを出す

### Prレビューチェック(管理者)

1. `sass-lint`が通っている前提なので`守ってほしいルール`が本当に守られているのか確認


## sass-lintのやり方

`yarn sass-lint`を叩く
問題なければ、`Done`と表示される。
失敗すればどの部分がおかしいか指摘さてるので、その部分を直すこと。

## 規約の修正フロー

1. 修正 or 追加したい箇所がある場合、修正フォーマットに沿ってPrを出す
フォーマットはissueを参照


## フォーマット

 ### フォーマット(lintでチェック)
  1. [インラインでは基本的に記述しない](#inline)
  1. [プロパティの記述順序](#prop_order)
  1. [ブロック単位のインデント](#block_indent)
  1. [プロパティ終端のセミコロン](#prop_last)
  1. [プロパティ終端のスペース](#prop_last_space)
  1. [セレクタ終端のスペース](#selector_last_space)
  1. [演算子前後のスペース](#space_around_operator)
  1. [カンマ後スペース](#space_after_comma)
  1. [空のセット](#no_empty_rulesets)
  1. [小数点の頭の「0」](#decimal_point)
  1. [URL値の引用符](#url_quote)
  1. [16進法のカラーコード](#HEX_color_code)
  1. [キーワードカラー](#no_color_keyword)
  1. [セレクタとプロパティの改行](#selector_prop_line)
  1. [タイプセレクタの指定方法](#type_selector)
  1. [コメントのルール](#comment)
  1. [borderの打ち消し](#border-none)
  1. [擬似クラス指定](#pseudo)
  1. [擬似クラス(余白の指定)](#pseudo_margin)
  1. [インポート](#import)
  1. [before-nesting](#nesting)
  2. [セレクタ後ろ要素のネスト](#force_element_nesting)
  3. [スタイルでのimportant禁止](#no_important)

 ### 守ってほしいルール

  1. 基本的にインライン(slim)には記述せず、css(scss)ファイルに書く。
  1. [ディレクトリ/ファイルの命名規則](#dir_file)
  1. [プロパティの宣言順序](#prop_order_sass)
  1. [定数の指定方法](#var)
  1. [メディアクエリ](#media)
  1. [font-size指定](#font_size)
  1. [余白のルール](#margin)
  2. [ショートハンドプロパティ](#short_hand)
  3. [line-heightの単位](#line-height)

***

## 守ってほしいルール

<h3 id="prop_order">プロパティ記述順序</h3>

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

 <h3 id="#prop_order_sass">プロパティの記述順序(sass)</h3>
 - `@include`などsass独特なプロパティ指定方法であっても、記述順序は統一する
 - その際プロパティの頭文字を見て判断すること。

 例)

 ```
 <NG>
 .Sample {
   width: 300px;
   @include font-size(12);
   background: #000;
 }

 <OK>
 .Sample {
   background: #000;
   @include font-size(12);
   width: 300px;
 }
 ```

 ***
 
  <h3 id="#prop_order_element_sass">要素(class/id)の記述順序</h3>
 - セレクタやエレメントやモディファイアを指定するときも、記述順序は統一する

 例)

 ```
 <NG>
 .sample {
  &__b {
   ...
  }
  
  &__a {
   ...
  }
 }
 
 .example {
  ...
 }

 <OK>
.Example {
  ...
}

.Example__A {}

.Example__B {} 
 ```

 ***

 <h3 id="var">定数の指定方法</h3>

 - グローバル(color.scssなど)の定数は原則大文字、スネークケース
 - ローカル定数(各scssファイルで使いたい変数)はscssのルールで書く
 - 定数の名前は主語が文頭、目的語が文末。 数字からや特殊文字から始まるのはNG
 - 使える記号は`_`と`-`のみ。

 ```
 /* グローバル */
 <NG>
 $bp_desktop: 750px;
 $color_main: #000;
 $color_red: #ab0835;
 $10_Width: 300px;
 $+color-red: red;

 <OK>
 $BP_DESKTOP: 750px;
 $COLOR_TRUNK_NORMAL: #...;
 $COLOR_TRUNK_GREEN: #...;
 ```

 <h3 id="media">メディアクエリ</h3>

 - scssのmixinで定義したものをincludeして使う
 - 指定したい場所単位で使う

 例)

 ```
 <ブレイクポイント以下>
.Sample {}

@include mq-small {
  .Sample {
    color: $COLOR_MAIN
  }
}
 ```

 ***

 <h3 id="font_size">font-sizeの指定</h3>

 - サイズの指定方法は「rem」を使う
1px＝0.75ptであることから、デバイスによってピクセル比が異なるので大きさが変わる
root(html)に依存するので、rootに基準となる大きさを決めておけば管理が楽になる

 - scssのmixinで定義したものをincludeして使う
 - `()`内に指定したい値を入れる

 - 参考 [CSSで知っておきたい、フォントサイズ指定の単位のすべて](https://ferret-plus.com/7062)

 ```
 <NG>
 .Sample {
   font-size: 12px;
 }

 <OK>
 .Sample {
   @include font-size(12);
 }
 ```

 ***

 <h3 id="margin">余白のルール</h3>

 - 外に余白をつけるときは、marginをつける
 - marginは原則下方向`margin-bottom`をつける / 横方向は`margin-right`をつける

 例)
 ```
 <NG>
 .Sample {
   margin: 20px 0 0 20px;
   or
   margin-right: 20px;
 }

 <OK>
 .Sample {
   margin: 0 20px 20px 0;
   or
   margin-right: 20px;
 }
 ```

 ***

<h3 id="short_hand">ショートハンドプロパティ</h3>

 - 同じプロパティが複数ある場合はショートハンドを使う。
 - 要注意なプロパティ `background`,`border`,`margin`,`padding`

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
 
 <h3 id="line-height">line-heightの単位</h3>

 - line-heightの単位はつけない

 例)
 ```
 <NG>
 line-height: 1.2em;
 line-height: 1.2px;
 line-height: 1.2rem;

 <OK>
 line-height: 1.2;
 ```

 ***

 <h3 id="prop_order">ディレクトリ/ファイルの命名規則</h3>

 - ディレクトリ/ファイル名は、原則小文字で付ける
 - 文頭に特殊文字、数字はつけない
 - application.scss(エントリーポイント)以外のscssファイルの文頭には `_` をつけてコンパイルしないようにする
 - sassファイルは１ファイル１コンポーネントとする

 例)

 ```
 <NG>
 `Sample.scss`
 `!sample.scss / 19sample.scss`

 <OK>
 `_sample.scss`
 `_sampleSample.scss`
 ```

 ***

## フォーマット

<h3 id="inline">基本的にインラインでは記述しない</h3>

- cssはインライン(slim)内には原則記述しない
- ~~ただし裏側の処理の部分で必要な場合は可~~ <= reactなので今後は原則書かない

例)

```
<NG>

.sample
css:
  .sample {
    width: 1059px;
  }

.sample style="width: 1059px;"
```

***

 <h3 id="block_indent">ブロック単位のインデント</h3>

 - 階層がわかりやすいように、ブロック単位でコードをインデントすること。

 例)

 ```
 <NG>
 .Block {
 &__Element {
 color: #333;
 display: block;
 }
 }

 <OK>
 .Block {
   &__Element {
     color: #333;
     display: block;
   }
 }
 ```

 ***

 <h3 id="prop_last">プロパティ終端のセミコロン</h3>

 - lint名 `trailing-semicolon`
 - すべてのプロパティの終端はセミコロンを書くこと。

 例)

 ```
 <NG>
 .Sample {
   display: block;
   height: 100px
 }

 <OK>
 .Sample {
   display: block;
   height: 100px;
 }

 ```

 ***

 <h3 id="prop_last_space">プロパティ名終端のスペース</h3>

 - すべてのプロパティ名の終端のコロンの後にスペースを入れる。

 例)

 ```
 <NG>
 .Sample {
   display:block;
 }

 <OK>
 .Sample {
   display: block;
 }

 ```

 ***

 <h3 id="selector_last_space">セレクタ終端のスペース</h3>

 - セレクタ終端に１つスペースを入れる。

 例)

 ```
 <NG>
 #Sample{
   margin-top: 1rem;
 }

 /* 改行は必要ない */
 #Sample
 {
   margin-top: 1rem;
 }

 <OK>
 #Sample {
   margin-top: 1rem;
 }

 ```

 ***

 <h3 id="space_after_comma">カンマ後スペース</h3>

 - lint名 `space-after-comma`
 - カンマ（,）のあとのスペースを入れる

 例)

 ```
 <NG>
 .Sample {
   box-shadow: 1px 1px $COLOR_MAIN,1px 1px $COLOR_MAIN;
 }

 <OK>
 .Sample {
   box-shadow: 1px 1px $COLOR_MAIN, 1px 1px $COLOR_MAIN;
 }

 ```

 ***

 <h3 id="space_around_operator">演算子前後のスペース</h3>

 - lint名 `space-around-operator`
 - 演算子（+, -, /, *, %, <, > ==, !=, <=, >=）の前後のスペースを入れる

 例)

 ```
 <NG>
 .Sample {
   width: 1000px+59px;
 }

 <OK>
 .Sample {
   width: 1000px + 59px;
 }

 ```

 ***

 <h3 id="no_empty_rulesets">空のセット</h3>

- lint名 `no-empty-rulesets`
- 空のスタイルセットはNG

 例)

 ```
 <NG>
 .Sample {

 }

 ```

 ***

 <h3 id="#decimal_point">小数点の「0」を省略/単位の表記</h3>

 - 小数点の頭の「0」は省略する。
 - 値が0の場合は単位を省略する。
 - 小数点以下の末尾の0は許可しない

 例)
 ```
 /* 小数点を省略 */
 <NG>
 .Sample {
   font-size: 0.8rem;
   opacity: 0.5;
   transition all 0.2s;
   width: 1059.0px;
 }

 <OK>
 .Sample {
   font-size: .8rem;
   opacity: .5;
   transition all .2s;
   width: 1059px;
 }

 /* 単位を省略 */
 <NG>
 .Sample {
   margin: 0px;
   padding: 0px;
 }

 <OK>
 .Sample {
   margin: 0;
   padding: 0;
 }
 ```

 ***

 <h3 id="url_quote">URL値の引用符</h3>

 - lint `url-quotes`
 - url()での指定において、""（クォーテーション）や''（シングルクォーテーション）などのURI値の引用符を省略すること。

 例)
 ```
 NG
 background-image: url("//www.google.com/css/go.css");

 OK
 background-image: url(//www.google.com/css/go.css);
 ```

 ***

 <h3 id="HEX_color_code">16進法カラーコード</h3>

 - lint名 `hex-length`
 - 16進法形式のカラーコードで3文字で表記できるものは3文字で。

 例)

 ```
 <NG>
 color: #eebbcc;

 <OK>
 color: #ebc;
 ```

 ***

 <h3 id="no_color_keyword">キーワードカラー</h3>

 - lint名 `no-color-keywords`
 - キーワードでカラーを指定しない
 - 定数で指定する場合もキーワードカラーはNG

 例)

 ```
 <NG>
 background-color: red;

 <OK>
 background-color: $COLOR_RED;
 ```

 ***

 <h3 id="prop_last">プロパティの改行</h3>

 - プロパティは改行して記述すること。

 例)

 ```
 <NG>
 .Sample {
   color: #444; display:block; width: 300px;
 }

 <OK>
 .Sample {
   color: #444;
   display: block;
   width: 300px;
 }

 ```

 ***

 <h3 id="selector_prop_line">セレクタとプロパティの改行</h3>

 - 別々のセレクタとプロパティがある場合は改行して書くこと。

 例)

 ```
 <NG>
 .Sample, .Hogehoge {
   display:block;
 }

 <OK>
 .Sample,
 .Hogehoge {
   display: block;
 }

 ```


 ***


 <h3 id="type_selector">タイプセレクタの指定方法</h3>

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

 <h3 id="comment">コメントのルール</h3>

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

 .Header{
  hogehoge...
 }

 /* end */

 /* main */

 .Main{
  hogehoge...
 }

 /* end */

 /* footer */

 .Footer{
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

 <h3 id="border_none">borderの打ち消し</h3>

 - `border`を打ち消す場合は`none`ではなく、`0`を指定する。
 `none`は`border-style` `0`は`border-width`
 styleのinitial(初期値)はnoneですが、widthのinitial(初期値)はmediumであり`0`ではない。
 よって、`border-style`を`none`にしても`border-width`は消えない

 例)

 ```
 <NG>
 .Sample {
   border-bottom: none;
 }

 <OK>
 .Sample {
   border-bottom: 0;
 }
 ```

 ***

<h3 id="pseudo">擬似クラス指定</h3>

 - `content`プロパティのクォーテーションはシングルで指定
 - `before`,`after`を指定する場合は前に`&::`をつける

 例)

 ```
 <NG>
 .Sample {
 
   &:after {
     content: ="";
   }
 }

 .Sample {
 
   sample::after {
     width: 1059px;
   }
 }

<OK>
.Sample {}

.Sample::after {
  content: ='';
}
 ```

 ***

 <h3 id="pseudo_margin">擬似クラス(余白の指定)</h3>

 - 原則`last-child`を使う。
 - 途中の要素を変更したい場合は`nth-of-type`と`nth-child`を使う
 - `nth-of-type`と`nth-child`の違いは要素（p, a, liなど）を判別して数えるかどうか。
 [擬似クラス nth-childとnth-of-type](https://qiita.com/kudo_kk/items/8277c1f0eae18e15dd64)

 例)
 ```
 <NG>

  /* scss */
 .Sample {
   margin-right: 20px;
   
   &:first-child {
     margin-right: 0;
   }
 }

 <OK>
.Sample {
  margin-right: 20px;
}

.Sample:last-child {
  margin-right: 0;
}
 ```

 ***

 ## クラスの命名ルール

 - 参考にしたもの[CSSのクラス名を決めるときに使うリストをつくりました](https://qiita.com/manabuyasuda/items/dbb76ed36970bec95470)
 - クラスめいは「ブロック」「エレメント」「状態」を想像しやすい端的な名前で表す。

例)

```
<NG>
青色のコメント → .blue
右寄せのブロック → .right

<OK>
青色のコメント → `.comment.comment_blue`
右寄せのブロック → .area.area_right
```

 - ~~「構造の意味の判斷がつかないもの」「構造の意味がないもの」に関しては汎用的なクラスを付ける。~~ <= 基本的にはジェネラルクラスは使用しない。変数を使用する
 - [ジェネラルクラスとは？](https://coliss.com/articles/build-websites/operation/css/200.html)

### pages(参考程度に)

- `FirmTimeLine` 企業タイムライン
- `Trainings` トレーニング一覧

### component

- `Button` ボタン
- `IconButton` アイコン付きのボタン
- `Heading` 見出し・表題
- `Thumbnail` サムネイル
- `Sort` ソート部分(職種絞り込みなど)
- `Skilltag` スキルタグ
- `Circle` 円のアイコンなど
- `Icon` アイコン
- `Notification` 通知
- `Datetime` 日付日時
- `Pagenation` ページネーション
- `Logo` ロゴ
- `Tab` タブ
- `Link` リンク
- `Carousel` 画像などをスライドさせる部分
- `Banner` バナー
- `Text` テキスト
- `Container` pages/partsらを囲む
- `Sidebar` サイドバー
- `Pickup` 選び出す
- `History` 更新履歴、沿革

- `Imgaes` トレーニング画像やインターンの画像
- `Media` テキスト+画像
- `Card/Area` レイアウトのためのボックス
- `SNS` snsをまとめるもの
- `GlobalHeader` ヘッダー
- `GlobalFooter` フッター
- `StudentNavigation` 学生側ナビゲーション
- `Breadcrumb` パンくずリスト

### element

- `Block__Inner` コンテンツを囲むもの
- `Block__Head` コンテンツの上部
- `Block__Foot` コンテンツの下部
- `Block__Left` コンテンツの左側
- `Block__Right` コンテンツの右側
- `Block__Center` コンテンツ中央
- `Block__Heading` コンテンツのタイトル
- `Block__Items` リストを囲むもの
- `Block__Item` リスト
- `Block__Texts` テキストを囲むもの
- `Block__Success` 完了時
- `Block__Label` ラベル

### modifier

- `-small` 小さい
- `-medium` 中間
- `-large` 大きい
- `-left` 左側
- `-right` 右側
- `-center` 真ん中
- `-student` TRUNK学生側カラー(グリーン)
- `-firm` TRUNK企業側カラー(ブルー)
- `-navy` TRUNKネイビー(ネイビー)
- `-gray` TRUNKグレー(グレー)
- `-next` 次
- `-prev` 前
- `-more` もっと
- `-current` 現在位置
- `-hidden` 非表示
- `-visible` 表示
- `-success` 完了時
- `-notice` 通知
- `-wanted` 募集
- `-full` 満員
- `-slightly` わずか(残数)

 ***

<h3 id="import">import</h3>

- importするファイル名にアンダースコアをつけない
- importするファイルの拡張子をつけるか
- applocatopn.scssはディレクトリ名でimportする

例) importするファイルの拡張子をつけるか
```
<NG>
@import 'sample.scss';
@import 'icon/sample.scss';

<OK>
@import 'sample';
@import 'icon/sample';
```

例) importするファイル名にアンダースコアをつけない
```
<NG>
@import '_sample';
@import '_icon/_sample';

<OK>
@import 'sample';
@import 'icon/sample';
```

例) applocatopn.scssはディレクトリ名でimportする
```
<NG>
@import 'atoms/index.scss'

<NG>
@import 'atoms'
```

***

<h3 id="no_important">スタイルでのimportant禁止</h3>

- lint名 `no-important`
- 強制的に上書きなどをする`important`は禁止
- jQueryなどのプラグインをいじらざる得ないときは要相談

例)

```
<NG>
.sample {
  width: 1059px !important;
}
```

***
