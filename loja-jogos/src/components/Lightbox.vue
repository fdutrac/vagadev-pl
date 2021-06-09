<template>
  <div class="lightbox-background" :class="{active: isActive}" >
    <div class="lightbox-container">
      <div class="lightbox-header">
        <img src="../assets/icons/close btn.png" class="lightbox-button" @click="closeLightbox" alt="">
      </div>
      <p class="lightbox-title">
        Pedido realizado com sucesso!
      </p>
      <div class="lightbox-body">
        <img class="lightbox-img" src="../assets/lightbox/mario-success.png" alt="">
      </div>
    </div>
  </div>
</template>

<script>
import eventBus from '@/eventBus';

export default {
  name: 'Lightbox',
  props: {
  },
  data() {
    return {
      isActive: false
    }
  },
  created() {
    eventBus.$on('gamebought', () => this.isActive = true);
  },
  methods: {
    closeLightbox(){
      this.isActive = false
    }
  }
}

</script>

<style scoped>
.lightbox-background {
  position:fixed;
  top:0;
  left: 0;
  z-index: 1;
  display: none;
  height: 100vh;
  width: 100vw;
  background: rgba(8, 65, 84, 0.62)
}

.lightbox-header {
  display: flex;
  height: 70px;
  padding: 15px;
  border-bottom: 1px solid #084154;
}

.lightbox-button {
  margin-left: auto;
  height: 50px;
  width: 50px;
}

.lightbox-title {
  color: #084154;
  font-weight: 300;
  font-size: 30px;
  width: 70%;
  text-align: center;
  margin:auto;
  background-color: #fff;
  margin-top: -20px
}

.lightbox-container {
  width: 370px;
  background-color: #ffffff;
  border-radius: 5px;
  justify-content: center;
}

.lightbox-body {
  display: flex;
  justify-content: center;
}

.lightbox-img {
  height: 80%;
  width: auto;
  margin-top: 50px;
}

.active {
  display: flex;
  align-items: center;
  justify-content: center;
}

</style>