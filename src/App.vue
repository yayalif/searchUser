<template>
  <div id="app">
    <!-- <search-user></search-user> -->
    <scroll></scroll>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import searchUser from './components/searchUser'
import scroll from './components/scroll'
export default {
  name: 'app',
  components: {
    HelloWorld,
    searchUser,
    scroll
  }
}
</script>

<style>
#app {
  width: 100vw;
  height: 100vh;

}
</style>
