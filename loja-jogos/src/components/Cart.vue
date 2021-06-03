<template>
  <div id="cart">
    <div class="cart-header" >
      <button class="close-btn" @click="hideCart">
        x
      </button>
      <h1 class="cart-title">Carrinho</h1>
      <div class="cart-icon">
        <img class="icon" src="../assets/icons/shopping-bag-solid.png">
        <div class="bagde">{{ gamesLenght }}</div>
      </div>

    </div>
    <div class="cart-body">
      <div v-for="game in games" :key="game" class="cart-item">
        <div class="cart-img--container">
          <img src="" class="cart-item--img" alt="">
        </div>
        <div>
          <p class="cart-item--title">{{game.title}}</p>
          <p class="cart-item--value">{{game.value}}</p>
        </div>
      </div>
    </div>
    <div class="cart-footer">
      <p>CALCULAR CEP</p>
      <div>
        <input type="text">
        <button class="cart-button">CALCULAR</button>
      </div>
      <div class="cart-address--container">
        <img src="" alt="">
        <div>
          <p>endereço</p>
          <p>FRETE GRÁTIS</p>
        </div>
      </div>
    </div>
    <div class="card-calc">

    </div>
    <button class="card-button">
      FINALIZAR PEDIDO
    </button>
  </div>
</template>

<script>
import eventBus from '@/eventBus';

export default {
  name: 'Cart',
  props: {
  },
  data() {
    return {
      isActive: false,
      games: []
    }
  },
  computed: {
    gamesLenght() {
      return this.games.length;
    }
  },
  created() {
    eventBus.$on('gamebought', game => {
      this.games.push(game)
    })
  },
  methods: {
    hideCart() {
      eventBus.$emit('closecart')
    },
  }
}
</script>

<style scoped>
#cart {
  color:#084154;
  background-color: #E5E5E5;
  min-width: 350px;
  position: absolute;
  display: block;
  right: 0;
  top:0;
  z-index: 1000;
  border-radius: 10px;
  align-items: center;
  padding: 0px 10px;
  ;
}

.cart-header {
  display: flex;
  align-items: center
}

.cart-icon {
  display: flex;
}

.cart-item {
  background-color: white;
  border-bottom: 1px solid rgb(165, 165, 165);
  padding: 5px 
}

.icon {
  width: 20px;
  height: 20px;
}

.icon:hover {
  opacity: 0.7;
  transition: 0.2s;
}


/* Responsividade para mobile  */

@media only screen and (max-width: 767px) {

}
</style>
