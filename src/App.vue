<template>
  <div id="app">
    <!-- <search-user></search-user> -->
    <!-- <scroll></scroll> -->
    <!-- <scroll2></scroll2> -->
    <scroll3></scroll3>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import searchUser from './components/searchUser'
import scroll from './components/scroll'
import scroll2 from './components/scroll2'
import scroll3 from './components/scroll3'
export default {
  name: 'app',
  components: {
    HelloWorld,
    searchUser,
    scroll,
    scroll2,// 原生js
    scroll3
  }
}
</script>

<style>
#app {
  width: 100vw;
  height: 100vh;

}
</style>
