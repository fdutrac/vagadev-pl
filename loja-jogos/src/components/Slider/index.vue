<template>
  <div>
    <transition name="fade">
      <div v-if="isActive" class="slider-content content-1">
        conteudo1
      </div>
      <div v-if="!isActive" class="slider-content content-2">
        conteudo2
      </div>
    </transition>
    <div @click="changeContent">
      botao
    </div>
  </div>
</template>

<script>

export default {
  name: 'Carousel',
  components: {  },
  data() {
    return { 
        isActive: false
      }
    },
  methods: {
    changeContent() {
      this.isActive = !this.isActive
    }
  }
}

</script>
<style>
.slider-content{
  height: 70vh;
}

.content-1 {
  transition: 0.5s;
  background-color: blue;
  transition: all 0.3s linear;
  background-image: url('../../assets/carousel/principal_banner_desktop 1.png');
}
.content-2 {
  transition: 0.5s;
  background-color: pink;
  transition: all 0.3s linear;
  background-image: url('../../assets/carousel/principal_banner_desktop_02.png');
}


</style>