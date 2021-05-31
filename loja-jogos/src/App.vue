<template>
  <div id="app">
      <Carousel />
      <Header />
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
      teste
    </div>
    <router-view/>
  </div>
</template>

<script>
import Header from '@/components/Header';
import Carousel from '@/components/Slider'

export default {
  name: 'App',
  components: {
    Header,
    Carousel
  }
}
</script>

<style>
@import './assets/main.css';

</style>
