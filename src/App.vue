<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <!-- <van-nav-bar
      title="标题"
      left-text="返回"
      right-text="按钮"
      left-arrow
      @click-left="onClickLeft"
      @click-right="onClickRight"
    /> -->
    <wedding />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Wedding from './components/Wedding'
import { NavBar, Toast } from "vant";

export default {
  name: "app",
  components: {
    [NavBar.name]: NavBar,
    Toast,
    wedding: Wedding
  },
  methods: {
    onClickLeft() {
      Toast('暂无后续逻辑~');
    },

    onClickRight() {
      Toast('暂无后续逻辑~');
    }
  }
};
</script>

<style>
body {
  background-color: #f4f4f4;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
