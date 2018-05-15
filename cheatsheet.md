# Fractal 構築手順

必須
node.js


### Fractalのためのディレクトリの準備
    cd 保存したい場所
    mkdir 任意のディレクトリ名

### まずはプロジェクト開始のためpackage.jsonファイルの作成
    npm init

### 次にFractalをインストール！
    npm install --save-dev @frctl/fractal
次にFractal CLI toolを入れる。
    npm i -g @frctl/fractal

### プロジェクト用のソースディレクトリを作る


ここまでのファイル構造…
    project
    ├── src
    │   ├── components
    │   └── docs
    └── package.json

### Fractalでごにょごにょするためにフラクタル用jsファイルを作成
    fractal.js

fractal.jsの中身
    'use strict';
    
    /*
    * Require the path module
    */
    const path = require('path');
    
    /*
     * Require the Fractal module
     */
    const fractal = module.exports = require('@frctl/fractal').create();
    
    /*
     * Give your project a title.
     */
    fractal.set('project.title', 'Style Guide');
    
    /*
     * Tell Fractal where to look for components.
     */
    fractal.components.set('path', path.join(__dirname, '/src/components'));
    
    /*
     * Tell Fractal where to look for documentation pages.
     */
    fractal.docs.set('path', path.join(__dirname, '/src/docs'));
    
    /*
     * Tell the Fractal web preview plugin where to look for static assets.
     */
    fractal.web.set('static.path', path.join(__dirname, '/public'));
    
    /* Specify a directory of static assets */
    fractal.web.set('static.path', __dirname + '/public');
    
    /* Set the static HTML build destination */
    fractal.web.set('builder.dest', __dirname + '/build');

ここまでのフォルダ構造
    project
    ├── src
    │   ├── components
    │   └── docs
    ├── fractal.js
    └── package.json

### コンポーネント用のhbsファイルを作成
    example.hbs

### ドキュメント用のmarkdownファイルを作成
    index.md

### 走らせる
先ずはsrcディレクトリに移動
    cd src
それからスタート用のコマンド↓ --syncを付けるとbrowsersyncのオートリフレッシュが使える。
    fractal start --sync
    略）
    fractal start -s

ポート指定はこちら↓　--portで任意の番号を指定可能
    fractal start --port 4000
    略）
    fractal start -p 4000


### 静的ファイルのディレクトリ
/public/
この中にcssファイルやjsファイルを格納する。
コンポーネントへの適用等…

### プレビューレイアウト用の読み込みファイル
    fractal.web.set('static.path', __dirname + '/public');
ウェブUI内から静的な資産を提供するには、使用することができstatic.path、資産のディレクトリへのパスを指定するには、上記設定オプションが必要。
ディレクトリ構造
    ├── components
    │   └── ...
    ├── public
    │   ├── css
    │   │   └── example.css
    │   └── js
    │       └── scripts.js

### 書き出し！
    fractal build