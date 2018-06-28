# webpack-simple-app

Vueのプロジェクトテンプレート

- vue独自のコンパイルシステムではなく、webpackというある程度馴染みのあるもので構成
- vue componentファイルから外部ファイルを読み込み
  - pug, stylus, typescriptに対応(独自に変更できる余地がある)
- scriptはclass記法を使えるようにvue-class-component導入

## vue独自のコンパイルシステムではなく、webpackというある程度馴染みのあるもので構成

```
npm -g i @vue/cli
vue init webpack-simple my-app
```

で可能だったが、メジャーバージョンアップが必要だったのでupgradeもした.
upgradeに伴い設定ファイルのイジる必要があった(コミットコメント参照)

Vue公式のcliから作られる公正なのだからvue-loaderは公式サポート内だと思う。全然メンテされてなかったけど。


## vue componentファイルから外部ファイルを読み込み

一番やりたかったことの一つ。
結局一つのファイルで、自分の使いたいフォーマットを複数書くのに対応したエディタなど存在しない。
重要なのはコンポーネントベースで分割することであって、コンポーネント単一ファイルで書くことではないと思う。

以下のように記述できること確認

```
// src/App.vue
<template lang="pug" src="./template.pug"></template>
<script lang="ts" src="./script.ts"></script>
<style lang="stylus" src="./style.styl"></style>
```

一応Vueの公式仕様の一部(ただ実装はvue-loaderが頑張ってる？vue-loaderも公式？)
https://jp.vuejs.org/v2/guide/single-file-components.html#%E9%96%A2%E5%BF%83%E3%81%AE%E5%88%86%E9%9B%A2%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6


## scriptはclass記法を使えるようにvue-class-component導入

javascriptのobjectというなんのcontextも無い世界でいろいろ書かされるというVueの嫌なところの一つ。
methodsキーにfunctionのarrayを登録していくなどとても悲しい。
やっていることがclass定義なのだから言語標準に乗るほうが良いと思ってVueのBasicUsageから少し外れる。

```
// src/script.ts
import Vue from 'vue';
import Component from 'vue-class-component';

@Component
export default class App extends Vue {
  msg: string = 'Welcome to Your Vue.js App';
}
```

BasicUsageではないが、Vue公式のサポート範囲内
https://jp.vuejs.org/v2/guide/typescript.html

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).
