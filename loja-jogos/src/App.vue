<template>
  <div id="app">
    <router-view/>
      <Header />
  </div>
</template>

<script>
import Header from '@/components/Header.vue';


export default {
  name: 'App',
  components: {
    Header,
  }
}
</script>

<style>
@import './assets/main.css';

</style>
