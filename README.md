# ディレクトリ構成
```bash
assets
├── foundation
│   ├── _base.scss
│   ├── _color.scss
│   ├── _font.scss
│   ├── _function.scss
│   ├── _mixin.scss
│   ├── _reset.scss
│   └── _variables.scss
├── layout
│   ├── _footer.scss
│   ├── _header.scss
│   └── _main.scss
├── object
│   ├── component
│   │   └── _button.scss
│   ├── project
│   │   └── _index.scss
│   └── utility
│       └── _utility.scss
└── style.scss

6 directories, 14 files
```

# ディレクトリ / ファイル説明
## 1. style.scss  
変数をまとめた`/foundation`を最初に読み込み  
`/layout`, `/component`, `/project`, `/utility`の順番で読み込む  
  ```scss
  // ==============================
  // foundation
  // ==============================
  @use "foundation/_font";
  @use "foundation/_color";
  @use "foundation/_variable";
  @use "foundation/_function";
  @use "foundation/_mixin";
  @use "foundation/_reset";
  @use "foundation/_base";

  // ===== foundationディレクトリ内のscssファイルの読み込み順に注意 =====
  // 1. _fontを最初に読み込む
  // 2. _color, _variable, _function (_mixin, _baseで使用する変数を使用する時のために先に読み込んでおく)
  // 3. _mixin
  // 4. _resetで全体のスタイルをリセットしてからベースである_baseを読み込む

  // ==============================
  // layout
  // ==============================
  @use 'layout/ファイル名';

  // ==============================
  // component
  // ==============================
  @use 'component/ファイル名';

  // ==============================
  // project
  // ==============================
  @use 'project/ファイル名';

  // ==============================
  // utility
  // ==============================
  @use 'utility/ファイル名';

  ```

## 2. foundation  
  - _base.scss  
  サイト全体のベースとなるスタイルと、`_reset.scss`でリセットしきれなかったスタイルを記述

  - _color.scss  
  サイト全体で使う色を変数として定義  
  色の接頭辞には`c-（color）`や`bg-（background）`、`text-`など、役割がわかるものを入れる

  - _font.scss  
  Webフォントを読み込む際に使用

  - _functions.scss  
  関数（`@function`）を定義

  - _mixin.scss  
  `@mixin`を定義

  - _reset.scss  
  `_reset.css`の拡張子をscssに変えてパーシャルにしただけのファイル(統一性を持たせるため拡張子はscss)  
  参考：Eric Meyer’s “Reset CSS” 2.0  → https://meyerweb.com/eric/tools/css/reset/  
  編集はしないでリセットしきれなかったスタイルや、デフォルトとして指定したいスタイルは`_base.scss`に追記  

  - _variables.scss  
  色以外で変数として管理したい値を定義  

## 3. layout  
サイトの大枠となる要素のスタイルを記述  
ファイル名はブロック要素をつける  
命名規則は`.l-*`  
  ```css
  .l-header, .l-footer__copyright, etc...
  ```  
  - _main.scss  
  `<body>`直下のサイト全体を囲むラッパー要素の`<div>`や`<main>`とその直下のインナーの`<div>`などのスタイルを管理  

## 4. object  
`/component`, `/project`, `/utility`の3ディレクトリに分けられる
  - component  
  サイト全体を通してどのページのどの部分でも同じ様に使える共通のモジュール定義  
  複数のページで使われている共通モジュール(パーツ) = コンポーネントと考えて良い  
  命名規則は`.c-*`  
    ```css
    .c-button__primary, .c-button__secondary, etc...  
    ```
    `component`内で`margin`は持たせない  
    余白をあける際は`project`のクラスでコンポーネントを囲ってそこに`margin`をいれる  

  - project  
  ページ固有のスタイルを定義  
  命名規則は`.p-*`  
  ページ名とセクション名をクラス名にして擬似スコープを作る  
    ```css
    .p-[ページ名]-[セクション名]__Element--Modifier
    .p-index-mv__heading, .p-about-profile__text, .p-compnay-info__list, etc...
    ```  
    各セクションの一番上のクラス名は`.p-[ページ名]-[セクション名]`となる
    ```html
    <section class="p-index-mv">
      <div class="p-index-mv__inner">
        <h1 class="p-index-mv__heading">...</h1>
        <div class="p-index-mv__mv">
          ...
    ```
    ファイル名は`_[ページ名].scss`となる
    ```
    index.scss (トップページ)
    _about.scss (aboutページ)
    _faq.scss (faqページ)
    ```
  - utility  
  スタイルの微調整に使うクラスを定義  
  命名規則は`.u-[Emmetのプロパティ＋値]`, `.u-[Emmetのプロパティ＋値]-[ブレイクポイント]-[min or max]`  
    1. Emmetのプロパティ  
       `margin-top: 10px;` → `mt10`  
       `width: 50%;` → `w50p`  

    2. ブレイクポイント  
       `foundation/_mixin.scss`に定義したブレイクポイント
    
    3. min or max  
       `min-width`で指定しているか`max-width`で指定しているかのメディアクエリ  
    
      ```scss
      .u-mt10-md-max  // margin-top: 10px;をmdブレイクポイント以下で適用
      .u-w50p-sm-min  // width: 50%;をsmブレイクポイント以上で適用
      .u-dn           // display: none;を全画面幅で適用
      ```
