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

## フォーマット
- cssはscssで書く
- インデントは２スペース
- プロパティの記述順序はABC順に
- ブロック単位のインデント
- プロパティ終端のセミコロンをつける
- プロパティ終端のスペースを入れる
- セレクタ終端のスペースを入れる
- cssにおいて`id`は使わない(jsのフックとして使用する場合は可)

## 例

 ### フォーマット
  1. [プロパティの記述順序](#prop_order)
  1. [ブロック単位のインデント](#block_indent)
  1. [プロパティ終端のセミコロン](#prop_last)
  1. [プロパティ終端のスペース](#prop_last_space)
  1. [セレクタ終端のスペース](#selector_last_space)

 ### その他指定
  1. [ショートハンドプロパティ](#short_hand)
  1. [小数点の頭の「0」](#decimal_point)
  1. [URI値の引用符](#url_quote)
  1. [16進法のカラーコード](#HEX_color_code)
  1. [セレクタとプロパティの改行](#selector_prop_line)
  1. [タイプセレクタの指定方法](#type_selector)
  1. [コメントのルール](#comment)
  1. [borderの打ち消し](#border-none)
  1. [Jsで扱う要素](#js_css)

 ### sass
  1. [プロパティの宣言順序](#prop_order_sass)
  1. [定数の指定方法](#var)
  1. [メディアクエリ](#media)
  1. [font-size指定](#font_size)
  1. [余白のルール](#margin)

<h3 id="validate">CSSバリデート</h3>
- 正確なcssなのか検証するため、[W3C CSS Validator](http://jigsaw.w3.org/css-validator/)でチェックする。

***

## フォーマット(例)

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

 <h3 id="block_indent">ブロック単位のインデント</h3>

 - 階層がわかりやすいように、ブロック単位でコードをインデントすること。

 例)

 ```
 <NG>
 .block {
 &__element {
 color: #333;
 display: block;
 }
 }

 <OK>
 .block {
   &__element {
     color: #333;
     display: block;
   }
 }
 ```

 ***

 <h3 id="prop_last">プロパティ終端のセミコロン</h3>

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

 <h3 id="prop_last_space">プロパティ名終端のスペース</h3>

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

 <h3 id="selector_last_space">セレクタ終端のスペース</h3>

 - セレクタ終端に１つスペースを入れる。

 例)

 ```
 <NG>
 #sample {
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

## その他指定(例)

 <h3 id="short_hand">ショートハンドプロパティ</h3>

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

 <h3 id="#decimal_point">小数点の「0」を省略/単位の表記</h3>

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

 <h3 id="url_quote">URL値の引用符</h3>

 - url()での指定において、""（ダブルコーテーション）や''（シングルコーテーション）などのURI値の引用符を省略すること。

 例)
 ```
 NG
 background-image: url("//www.google.com/css/go.css");

 OK
 background-image: url(//www.google.com/css/go.css);
 ```

 ***

 <h3 id="HEX_color_code">16進法カラーコード</h3>

 - 16進法形式のカラーコードで3文字で表記できるものは3文字で。

 例)

 ```
 <NG>
 color: #eebbcc;

 <OK>
 color: #ebc;
 ```

 ***

 <h3 id="prop_last">プロパティの改行</h3>

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

 <h3 id="selector_prop_line">セレクタとプロパティの改行</h3>

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

 <h3 id="border_none">borderの打ち消し</h3>

 - `border`を打ち消す場合は`none`ではなく、`0`を指定する。
 `none`は`border-style` `0`は`border-width`
 styleのinitial(初期値)はnoneですが、widthのinitial(初期値)はmediumであり`0`ではない。
 よって、`border-style`を`none`にしても`border-width`は消えない

 例)

 ```
 <NG>
 .sample {
   border-bottom: none;
 }

 <OK>
 .sample {
   border-bottom: 0;
 }
 ```

 ***

 <h3 id="js_css">Jsで扱う要素</h3>

 - jsでアニメーションをさせたり、jsで扱う部分は文頭に「js-」をつける
 - 「js-」をつけていない要素はjsで扱わない。
 - 「js-」のclassにstyleは記述しない。トリガーとしてだけ使う

 例)

 ```

 <NG>
 /* styleを当てる */
 .js-hoge {
   color: #000;
 }


 <OK>
 .js-hogehoge
 #js-hogehoge
 ```


 ***


 <h3 id="margin">余白のルール</h3>

 - 外に余白をつけるときは、marginをつける
 - marginは原則下方向`margin-bottom`をつける / 横方向は`margin-right`をつける

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

 ***

 ## 擬似クラス(余白の指定)

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

 ***

 ## クラスの命名ルール

 - 参考にしたもの[CSSのクラス名を決めるときに使うリストをつくりました](https://qiita.com/manabuyasuda/items/dbb76ed36970bec95470)

### 比較

- `student` 学生側にしかないもの
- `global` 全体的に使うもの

### pages(コンテンツ/ブロック)

- `timeline` タイムライン
- `training` トレーニング一覧
- `training-detail` トレーニング詳細
- `intern` インターン一覧
- `intern-detail` インターン詳細
- `dashbord` ダッシュボード
- `job` 求人ページ
- `mypage` レジュメ
- `myproject` プロジェクト詳細
- `chat` チャット画面
- `home` トップページ
- `announce` お知らせ画面
- `form` プロフィール編集/プロジェクト登録/職歴登録・編集
- `tutorial` チュートリアル画面
- `student-firm` 学生側の企業一覧
- `student-firm-detail` 学生側の企業詳細
- `firm` 企業側ページ
- `admin` 管理側ページ
- `guide` ガイドページ

### parts(コンテンツ/ブロック)

- `button` ボタン
- `icon-button` アイコン付きのボタン
- `buttons` ボタンを囲むもの
- `heading` 見出し・表題
- `thumbnail` サムネイル
- `sort` ソート部分(職種絞り込みなど)
- `skilltag` スキルタグ
- `circle` 円のアイコンなど
- `icon` アイコン
- `notification` 通知
- `datetime` 日付日時
- `pagenation` ページネーション
- `logo` ロゴ
- `tab` タブ
- `link` リンク
- `carousel` 画像などをスライドさせる部分
- `banner` バナー
- `text` テキスト

### レイアウトパターン(partsを組み合わせて使うもの)
- `imgaes` トレーニング画像やインターンの画像
- `media` テキスト+画像
- `card` コンテンツを囲むもの
- `texts` テキストを囲むもの
- `sns` snsをまとめるもの
- `global-header` ヘッダー
- `global-footer` フッター
- `student-navigation` 学生側ナビゲーション
- `breadcrumb` パンくずリスト

### element

- `inner` コンテンツを囲むもの
- `head` コンテンツの上部
- `foot` コンテンツの下部
- `left` コンテンツの左側
- `right` コンテンツの右側
- `center` コンテンツ中央
- `heading` コンテンツのタイトル
- `items` リストを囲むもの
- `item` リスト

### modifier

- `small` 小さい
- `medium` 中間
- `large` 大きい
- `left` 左側
- `right` 右側
- `center` 真ん中
- `green` TRUNKカラー(グリーン)
- 'blue' TRUNKカラー(ブルー)
- 'navy' TRUNKカラー(ネイビー)
- 'gray' TRUNKカラー(グレー)

 ***

## sass(例)

 <h3 id="#prop_order_sass">プロパティの記述順序(sass)</h3>
 - `@include`などsass独特なプロパティ指定方法であっても、記述順序は統一する
 - その際プロパティの頭文字を見て判断すること。

 例)

 ```
 <NG>
 .sample {
   width: 300px;
   @include font-size(12);
   background: #000;
 }

 <OK>
 .sample {
   background: #000;
   @include font-size(12);
   width: 300px;
 }
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
 $COLOR_MAIN: #000;
 $COLOR_RED: #ab0835;
 ```

 <h3 id="media">メディアクエリ</h3>

 - scssのmixinで定義したものをincludeして使う
 - 指定したい場所単位で使う

 例)

 ```
 <ブレイクポイント以下>
 .sample1 {
   @include mq-small {
     color: $COLOR_MAIN
   }
 }

 .sample2 {
   @include mq-small {
     color: $COLOR_MAIN
   }
 }

 <ブレイクポイント以上>
 .sample1 {
   @include mq-large {
     color: $COLOR_MAIN
   }
 }

 .sample2 {
   @include mq-large {
     color: $COLOR_MAIN
   }
 }

 ```

 ***

 <h3 id="font_size">font-sizeの指定</h3>

 - サイズの指定方法は「rem」を使う
 ...単に大きさを`px`と`rem`指定した差はありません。しかし、`px`は絶対指定なので、`font-family`やブラウザ毎の違いで大きさにムラが出てしまう。
 `rem`はroot(html)を基準に大きさを計算するので、rootの大きさを決めてしまえば、大きさを統一出来る。

 - scssのmixinで定義したものをincludeして使う
 - `()`内に指定したい値を入れる

 - 参考 [CSSで知っておきたい、フォントサイズ指定の単位のすべて](https://ferret-plus.com/7062)

 ```
 <NG>
 .sample {
   font-size: 12px;
 }

 <OK>
 .sample {
   @include font-size(12);
 }
 ```

 ***
