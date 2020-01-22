<template>
  <div class="home">
    <div>{{ text }}</div>
    <div>{{ num + ( num * tax ) }}</div>
    <div>{{ flag ? "OK" : "NG" }}</div>
    <div>{{ howMuch }}</div>
    <div v-show="vShowFlag">v-show</div>
    <div v-if="vIfFlag">v-if</div>
    <ul>
      <li v-for="(item, index) in listItems" :key="index">{{ item }}</li>
    </ul>
    <input v-model="inputText" />
    <div>{{ inputText }}</div>
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App" :propValue="10"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
    HelloWorld
  },
  data: function() {
    return {
      text: "price0000000000",
      num: 200,
      tax: 0.1,
      flag: true,
      vShowFlag: true,
      vIfFlag: true,
      listItems: ["apple", "banana", "orange"],
      inputText: ""
    }
  },
  computed: {
    howMuch() {
      return this.text + " is " + (this.num + (this.num * this.tax))
    }
  },
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
