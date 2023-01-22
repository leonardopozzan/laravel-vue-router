<template>
  <header>
    <AppHeader></AppHeader>
  </header>
  <main>
    <div class="container">
      <router-view></router-view>
    </div>
  </main>
</template>

<script>
import AppHeader from './components/HeaderComponent.vue';
  export default {
    name: 'App',
    components:{
      AppHeader
    }
  }
</script>

<style lang="scss" scoped>
@use './assets/style/variables' as *;

main{
  background-color: $background-grey;
  min-height: calc(100vh - 100px);
}
</style>