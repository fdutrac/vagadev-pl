<template>
  <div class="cart-container">
    <div id="cart">
      <div class="cart-header" >
        <button class="close-btn" @click="hideCart">
          <img class="icon" src="../assets/icons/close icon.png">
        </button>
        <h1 class="cart-title">Carrinho</h1>
        <div class="cart-icon">
          <img class="icon" src="../assets/icons/shopping-bag-solid blue.png">
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
        <p>CALCULAR FRETE</p>
        <div class="cart-input">
          <input v-model="zipcode" @keydown="filterEntry($event)" type="text" maxlength="8" placeholder="Digite seu cep">
          <button class="cart-button" @click="searchAddress">CALCULAR</button>
        </div>
        <div class="cart-address--container" v-if="address.street">
          <img src="../assets/icons/location.png" class="icon" alt="">
          <div>
            <p class="address-text">{{ address.street + ', ' + address.neighborhood }}</p>
            <p class="address-text">{{ address.city + ', ' + address.state }}</p>
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
  </div>
</template>

<script>
import eventBus from '@/eventBus';
import axios from 'axios';

export default {
  name: 'Cart',
  props: {
  },
  data() {
    return {
      isActive: false,
      games: [],
      zipcode: '',
      address: {
        street: '',
        neighborhood: '',
        city: '',
        state: '',
      }
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

    viacepURL(cep) {
      return `https://viacep.com.br/ws/${cep}/json/`;
    },

    filterEntry(e) {
      if (
        // Permite somente numeros
        (e.keyCode >= 48 && e.keyCode <= 57) || (e.keyCode >= 96 && e.keyCode <= 105)
        // Permite teclas lado direito, esquerdo, delete, backspace, tab e enter
        || /^(8|9|13|46|37|39|17)$/.test(e.keyCode)
        // Permite ctrl+ c,v,x,a,z
        || (/^(67|86|88|65|90)$/.test(e.keyCode) && e.ctrlKey)
      ) return;
      e.preventDefault();
      e.stopPropagation();
    },
    searchAddress() {
      this.address.street = '';
      this.address.neighborhood = '';
      this.address.city = '';
      this.address.state = '';

      if (!(/^[0-9]{8}$/).test(this.zipcode)) return;
      axios.get(this.viacepURL(this.zipcode)).then((response) => {
        this.address.street = response.data.logradouro;
        this.address.neighborhood = response.data.bairro;
        this.address.city = response.data.localidade;
        this.address.state = response.data.uf;
      });
      console.log('=====', this.address)
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
  border: none;
  cursor: pointer
}

input {
  padding: 0 5px;
  border: none;
  color: #084154;
  cursor: pointer
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

.cart-container {
  position: fixed;
  top: 0;
  right: 0;
  height: 100vh;
  width: 100vw;
}

#cart {
  color:#084154;
  background-color: #ffffff;
  min-width: 350px;
  position: absolute;
  top: 0;
  right: 0;
  display: block;
  z-index: 1000;
  border-radius: 10px;
  align-items: center;
  padding: 15px;
  box-shadow: 0px 3px 3px 3px rgba(0, 0, 0, 0.363);
  overflow-y:scroll;
  overflow-x:unset;
  max-height: 600px;
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
.cart-icon .icon {
  margin-right: 10px;
}

.close-btn {
  width: 25px;
  height: 25px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #F55959;
  border-radius: 50%
}

.close-btn:hover {
  background-color: #9c3b3b;
  cursor: pointer
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

.address-text {
  font-size: 12px;
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
  .cart-container {
    background-color: rgba(8, 65, 84, 0.384);
  }

  #cart {
    top: 30px;
    right: 0;
    left: 0;
    margin-right: auto;
    margin-left: auto;
    max-height: 87vh;
    max-width: 400px;
  }
}

</style>
