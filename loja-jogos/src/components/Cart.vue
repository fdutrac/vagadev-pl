<template>
  <div id="cart">
    <div class="cart-header" >
      <button class="close-btn" @click="hideCart">
        <img class="icon" src="../assets/icons/close icon.png">
      </button>
      <h1 class="cart-title">Carrinho</h1>
      <div class="cart-icon">
        <img class="icon" src="../assets/icons/shopping-bag-solid.png">
        <div class="bagde">{{ gamesLenght }}</div>
      </div>

    </div>
    <div class="cart-body">
      <div class="empty" v-if="games.length === 0">
        Você ainda não adicionou nada aqui :(
      </div>
      <div v-for="game in games" :key="game.title" class="cart-item">
        <div class="cart-img--container">
          <img :src="`products/${game.img}`" class="cart-item--img" alt="">
        </div>
        <div>
          <p class="cart-item--title">{{game.title}}</p>
          <p class="cart-item--value">R$ {{game.value}}</p>
        </div>
      </div>
    </div>
    <div class="cart-footer">
      <p>CALCULAR CEP</p>
      <div class="cart-input">
        <input type="text" placeholder="Digite seu cep">
        <button class="cart-button">CALCULAR</button>
      </div>
      <div class="cart-address--container">
        <img src="../assets/icons/location.png" class="icon" alt="">
        <div>
          <p>endereço</p>
          <p><strong>FRETE GRÁTIS</strong></p>
        </div>
      </div>
    </div>
    <div v-if="games.length > 0" class="cart-calc">
      <p>
        TOTAL: <strong>{{ calcTotal }}</strong>
      </p>
      <p>
        OU: <strong>12X</strong> de <strong>{{ calcInstallments }}</strong>
      </p>
    </div>
    <button class="cart-button">
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
      games: [],
      address: ''
    }
  },
  computed: {
    gamesLenght() {
      return this.games.length;
    },
    calcTotal() {
      let total = 0
      this.games.forEach(game => {
        total += parseInt(game.value)
      });
      const formatter = new Intl.NumberFormat('pt-BR', {
        style: 'currency',
        currency: 'BRL'
      })
      return formatter.format(total)
    },
    calcInstallments() {
      let total = 0
      this.games.forEach(game => {
        total += parseInt(game.value)
      });
      total = (total/12)
      const formatter = new Intl.NumberFormat('pt-BR', {
        style: 'currency',
        currency: 'BRL'
      })
      return formatter.format(total)
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
p {
  margin: 5px 0px;
  font-size: 14px;
}

h1 {
  margin: 10px;
}

button {
  border: none
}

input {
  padding: 0 5px;
  border: none;
  color: #084154;
  /* width: 60% */
}

.bagde {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 22px;
  height: 22px;
  background-color: #3EC6E0;
  border-radius: 50%;
  font-size: 12px;
  font-weight: bold;
  color: white
}

input:focus {
  outline: none
}

::placeholder { /* Chrome, Firefox, Opera, Safari 10.1+ */
  color: #084154;
  opacity: 1; /* Firefox */
}

:-ms-input-placeholder { /* Internet Explorer 10-11 */
  color: #084154;
}

::-ms-input-placeholder { /* Microsoft Edge */
  color: #084154;
}

.empty {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100px;
}

#cart {
  color:#084154;
  background-color: #ffffff;
  min-width: 350px;
  position: absolute;
  display: block;
  right: 0;
  top:0;
  z-index: 1000;
  border-radius: 10px;
  align-items: center;
  padding: 15px;
  ;
}


.cart-header {
  position: relative;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-left: 15px;
  margin: 0px;
}

.cart-title {
  font-weight: 400;
}

.cart-icon {
  display: flex;
}

.close-btn {
  position: absolute;
  left: -27px;
  width: 25px;
  height: 25px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #F55959;
  border-radius: 50%
}
.close-btn .icon {
  width: 12px;
  height: 12px;
}

.cart-item {
  display: flex;
  align-items: center;
  border-bottom: 1px solid rgb(165, 165, 165);
  padding: 10px 0px;
}

.cart-item--img {
  max-width: 150px;
  height: auto;
}

.cart-item--value {
  font-weight: bold;
}

.cart-input {
  border: 2px solid #084154;
  border-radius: 5px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 5px
}

.cart-button {
  background-color: #3EC6E0;
  font-weight: bold;
  color: white;
  padding: 10px;
  width: 100%;
  border-radius: 5px;
}

.cart-button:hover {
  background-color: #0e6785;
  transition: 0.3s;
}

.cart-address--container {
  display: flex;
  /* margin-top: 10px; */
  align-items: center;
  font-size: 12px;
  min-height: 90px;
  border-bottom: 1px solid rgb(165, 165, 165);
}

.cart-footer {
  padding: 10px 0px;
}

.cart-calc {
  padding: 10px 0px;
}

.cart-address--container .icon {
  width: 30px;
  height: 30px;
  margin-right: 10px;
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
