# ディレクトリ構成
```bash
assets
├── foundation
│   ├── _base.scss
│   ├── _color.scss
│   ├── _font.scss
│   ├── _function.scss
│   ├── _mixin.scss
│   ├── _reset.scss
│   └── _variables.scss
├── layout
│   ├── _footer.scss
│   ├── _header.scss
│   └── _main.scss
└── obejct
    ├── component
    │   └── _button.scss
    ├── project
    │   └── _index.scss
    ├── utility
    └── _utility.scss

6 directories, 13 files
```

# ディレクトリ / ファイル説明
- foundation  
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
  編集はしない
  参考：Eric Meyer’s “Reset CSS” 2.0  
  https://meyerweb.com/eric/tools/css/reset/  
  リセットしきれなかったスタイルや、デフォルトとして指定したいスタイルは`_base.scss`に追記  

  - _variables.scss  
  色以外で変数として管理したい値を定義
- layout  

- object  
  - component  

  - layout  

  - object  

# クラス命名規則
