<template>
  <header>
    <AppHeader></AppHeader>
  </header>
  <main>
    <div class="my-container">
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
.my-container{
  width: 80%;
  margin: auto;
}
main{
  background-color: rgb(239, 239, 239);
}
</style>