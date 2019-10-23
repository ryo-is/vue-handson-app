
この記事は 11/02 に開催される関西フロンエンドカンファレンス2019内のハンズオントラック「Vue.js 超入門ハンズオン」の資料です。

## 目的

今回のハンズオンの目的は「Vue.jsの超基本的なことを学んで、これからVue.jsを使っていくためのきっかけを掴む」ということを目的としています。
このハンズオンでVue.jsのすべてを学べるということではないのでご了承ください。

## 事前準備(5分)

### Nodejs のインストール

[公式サイト](https://nodejs.org/ja/)からインストーラをダウンロードしてください。
※他の方法でも問題ないです。

### Vue-CLI のインストール

```
$ npm i -g @vue/cli
$ vue --version
@vue/cli 4.0.5
```

### プロジェクトの作成

CLIの `vue create` コマンドを使って、Vueのプロジェクトを作成していきます。

```terminal
$ vue create vue-handson-app
Vue CLI v3.11.0
? Please pick a preset: (Use arrow keys)
❯ Manually select features
? Check the features needed for your project: (Press <space> to select, <a> to toggle all, <i> to invert selection)
❯◉ Babel
 ◯ TypeScript
 ◯ Progressive Web App (PWA) Support
 ◉ Router
 ◯ Vuex
 ◯ CSS Pre-processors
 ◉ Linter / Formatter
 ◯ Unit Testing
 ◯ E2E Testing
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Pick a linter / formatter config: (Use arrow keys)
❯ ESLint with error prevention only 
  ESLint + Airbnb config 
  ESLint + Standard config 
  ESLint + Prettier 
? Pick additional lint features: (Press <space> to select, <a> to toggle all, <i> to invert selection)
❯◉ Lint on save
 ◯ Lint and fix on commit
? Where do you prefer placing config for Babel, PostCSS, ESLint, etc.? (Use arrow keys)
❯ In dedicated config files 
  In package.json 
? Save this as a preset for future projects? (y/N) No
```

### アプリケーションを起動する

```terminal
$ cd vue-handson-app
$ yarn serve
```

`yarn serve` 実行後にブラウザで `localhost:8080` を開くと、下の画像のような画面が表示されればOKです。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/95875/117f2164-043e-ce13-e7a6-e53d088cdc39.png)

これで事前準備は完了です。
本編は当日にご案内します。