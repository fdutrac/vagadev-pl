<template>
  <div class="card">
    <div class="card-img--container">
      <img :src="`products/${game.img}`" class="card-img" alt=""/>
    </div>
    <div class="card-description">
      <p class="card-title">
        {{ game.title }}
      </p>
      <p class="card-value">
        R$ {{ game.value }}
      </p>
      <div class="card-button--container">
        <button class="card-button" :class="{bought: bought ? 'bought' : ''}" @click="isBought">
          {{ bought ? 'COMPRADO!' : 'COMPRAR' }}
        </button>
        <img v-if="bought" src="../assets/icons/bought.png" class="bought-img" alt="">
      </div>
    </div>
  </div>
</template>

<script>
import eventBus from '@/eventBus';

export default {
  name: 'Spotlight',
  props: {
    game: {
      img: '',
      title: '',
      value: '',
    },
  },
   data() {
    return {
      bought: false

   }
  }, 
  methods: {
    isBought() {
      if(this.bought === false) {
        eventBus.$emit('gamebought', this.game);
        return this.bought = true;
      }
    },
  }
}

</script>
<style scoped>
p {
  color: #084154
}

.card-button--container {
  position: relative;
}

.card-button {
  display: flex;
  margin: auto;
  border: 0;
  border-radius: 5px;
  background-color: #3EC6E0;
  width: 70%;
  height: 45px;
  justify-content: center;
  align-items: center;
  font-weight: 900;
  color: white
}

.card-button:hover {
  transition: 0.3s;
  background-color: #0b5269;
  width: 68%;
  height: 42px;
  margin: 3px auto
}

.cart-title {
  font-size: 14px;

}

.card-value {
  font-size: 18px;
  font-weight: 900;
}

.card-description {
  display: block;
  padding: 20px;
}

.card {
  max-width: 300px;
  min-height: auto;
  margin: 10px;
  box-shadow: 0px 4px 20px 7px rgba(0, 0, 0, 0.07);
  border-radius: 10px;
  overflow: hidden;
  opacity: 1;
}

.card-img--container {
  display: flex;
  justify-content: center;
  background-color: white;
  border-bottom: solid 2px #3EC6E0;
}

.card-img {
  max-width: 80%;
  height: auto;
}
.bought {
  background-color: #084154;
  justify-content: start;
  padding-left: 20px;
}

.bought-img {
  position: absolute;
  top: -34px;
  right: 16%
}
.bought:hover {
  width: 70%;
  height: 45px;
  margin: auto;
  background-color: #084154;
}

</style>