
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
3.11.0
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

## Vueの説明(10分)

https://docs.google.com/presentation/d/1i5JgkV4qswTzan0i2UTxHR5W8qpvFKkkzrH5OqzK3QU/edit?usp=sharing

## ソースコードを見てみる(5分)

`App.vue` や `Home.vue` などの vue ファイルを見ていきましょう。

## データバインディング(5分)

`{{ text }}` のような書き方をすると、コンポーネントのdata内で宣言している変数を表示することができます。

```vue
<template>
  <h1>{{ text }}</h1>
</template>

<script>
export default {
  data: function() {
    return {
      text: "price"
    }
  }
}
</script>
```

またこのように単一であればJavaScript式を書くこともできます。

```vue
<template>
  <div>{{ num + ( num * tax ) }}</div>
  <div>{{ flag ? "OK" : "NG" }}</div>
</template>

<script>
export default {
  data: function() {
    return {
      num: 100,
      tax: 0.08,
      flag: true
    }
  }
}
</script>
```

## 算出プロパティ(5分)

先程のようにテンプレート内に書くのはすごく便利なのですが、あまりにも複雑なことをするのはおすすめできません。
複雑な処理をする場合は算出プロパティ( `computed` )を使いましょう。

```vue
<template>
  <div>{{ howMuch }}</div>
</template>

<script>
export default {
  data: function() {
    return {
      text: "price",
      num: 100,
      tax: 0.08
    }
  },
  computed: {
    howMuch() {
      return this.text + " is " + (this.num + (this.num * this.tax))
    }
  }
}
</script>
```

## ディレクティブ(15分)

### 要素の表示/非表示

要素の表示/非表示を動的に切り替えたいというときに `v-if` や `v-show` を使います。
条件がtrueなら要素を表示、falseなら非表示になります。

```vue
<template>
  <div v-show="vShowFlag">v-show</div>
  <div v-if="vIfFlag">v-if</div>
</template>

<script>
export default {
  data: function() {
    return {
      vShowFlag: false,
      vIfFlag: true
    }
  }
}
</script>
```

どちらも見た目上の挙動は同じなのですが、内部的な挙動は異なります。

* `v-if` は要素そのものを生成/削除して切り替えます。
* `v-show` はCSSで表示を切り替えます。

なので `v-if` は表示を切り替えるたびに要素が増えたり減ったりするので、`v-show` に比べて切替時のコストが少し高くなってしまいます。
ただ初期非表示の場合は `v-if` を使うと要素が描画されないので、初期表示時のコストを少し節約することができます。
うまく使い分けることが大切です。
`v-show` は `display: none` 、 `v-if` は `<!---->` とコメント扱いになっている
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/95875/954cd108-76cd-2871-3ee9-0fcde8e151af.png)

### 動的に要素を生成する

リストを作成するときなど、同じタグを複数作成する際に便利なのが `v-for` というディレクティブです。

```vue
<template>
  <ui>
    <li v-for="(item, index) in listItems" :key="index">{{ item }}</li>
  </ui>
</template>

<script>
export default {
  data: function() {
    return {
      listItems: ["apple", "banana", "orange"]
    }
  }
}
</script>
```

### inputの値

form内のinput要素の値を取得したい場合には `v-model` を使います。
`v-model` の値は入力があるたびに動的に変化し続けます。その値をバインディングすると変化しているのがわかります。

```vue
<template>
  <input v-model="inputText" />
  <div>{{ inputText }}</div>
</template>

<script>
export default {
  data: function() {
    return {
      inputText: ""
    }
  }
}
</script>
```

## Component間でデータの受け渡しをする(5分)

色んなコンポーネントを配置していくと、コンポーネントからコンポーネントに何かしらの値を渡したくなる場合があると思います。
そんなときはプロパティ( `prop` )で渡すことができます。
次の例は `Home.vue` から `HelloWorld.vue` に値を渡している部分を抽出したものです。

```vue:Home.vue
<template>
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  components: {
    HelloWorld
  },
}
</script>
```

```vue:HelloWorld.vue
<template>
  <h1>{{ msg }}</h1>
</template>

<script>
export default {
  props: {
    msg: String
  }
}
</script>
```

プロパティを増やしてみましょう。またプロパティに対してデフォルト値を設定することもできます。

```vue:Home.vue
<template>
  <HelloWorld msg="Welcome to Your Vue.js App" :propValue="10"/>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  components: {
    HelloWorld
  },
}
</script>
```

```vue:HelloWorld.vue
<template>
  <h1>{{ msg }} / {{ propValue }}</h1>
</template>

<script>
export default {
  props: {
    msg: String,
    propValue: {
      type: Number,
      default: 0
    }
  }
}
</script>
```

## LifeCycleHooks(5分)

コンポーネントが生成されてから削除されるまでの特定のタイミングで処理を実行させることができます。
例えば「コンポーネントが生成されたタイミングでAPIを呼びたい」や「コンポーネントが破棄される前に処理を実行したい」などのときに使います。

```vue
<script>
export default {
  created() {
    console.log("created!")
  },
  mounted() {
    console.log("mounted")
  },
  beforeDestroy() {
    console.log("before destroy")
  }
}
</script>
```

## アプリをビルドする(3分)

せっかく作ったアプリもこのままではWebアプリケーションとしてホスティングすることができません。
ホスティングできるようにビルドする必要があります。
`build` コマンドを実行してビルドしましょう。

```terminal
$ npm run build
```

処理が完了すると `dist` ディレクトリが生成されていて、その中にビルド後のファイルが入っています。
実際にホスティングする際にはこのディレクトリ内のファイルをアップロードすることになります。
もし firebase や netlify などのサービスのアカウントをお持ちの方は試してみてください。

## おつかれさまでした！

コンテンツはこれで終わりになります。
ですが時間の都合上取り上げることができなかった題材がたくさんあります…
TypeScript だったり ESLint/Prettier だったり Vuex だったりあげだしたらキリがないんですが…
今回のハンズオンを通してVueを使い始めるきっかけになれば幸いです！
