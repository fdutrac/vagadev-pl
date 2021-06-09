<template>
  <nav id="header" :class="{solidBG: isActive}">
    <div class="brand">
      <div class="dropdown">
        <button class="dropbtn" @click="showMenu">
          <img class="icon" :src="changeIcon()">
        </button>
        <div class="dropdown-content" :class="{active: isActive}">
          <div class="dropdown-section" href="#">
            <span class="dropdown-title" href="">Luta</span>
            <a class="dropdown-item" href="">Mortal Kombat</a>
            <a class="dropdown-item" href="">Smash Bros</a>
            <a class="dropdown-item" href="">Killer Instinct</a>
            <a class="dropdown-item" href="">DBZ Kakarot</a>
          </div>
          <div class="dropdown-section" href="#">
            <span class="dropdown-title" href="">Ação / Aventura</span>
            <a class="dropdown-item" href="">GTA V</a>
            <a class="dropdown-item" href="">Tomb Raider</a>
            <a class="dropdown-item" href="">HALO</a>
            <a class="dropdown-item" href="">Call of Duty</a>
          </div>
          <div class="dropdown-section" href="#">
            <a class="dropdown-title" href="">Corrida</a>
            <a class="dropdown-item" href="">NEED for SPEED</a>
            <a class="dropdown-item" href="">Forza Horizon</a>
          </div>
        </div>
      </div>
      <img class="logo" src="../assets/brand.png" alt="">
    </div>
    <ul>
      <li class="border">
        <img class="icon" src="../assets/icons/paper-plane.png">
        <span>
        CONTATO
        </span>
      </li>
      <li class="border">
        <img class="icon" src="../assets/icons/search-solid.png">
        <span>
        BUSCAR
        </span>
      </li>
      <li @click="openCart">
        <img class="icon" src="../assets/icons/shopping-bag-solid.png">
        <div class="badge">{{ counter }}</div>
      </li>
    </ul>
    <transition name="slide-fade">
      <Cart class="cart" v-show="cartActive" />
    </transition>
  </nav>
</template>

<script>
import eventBus from '@/eventBus';
import Cart from './Cart.vue';

export default {
  name: 'Header',
  props: {
  },
  components: {
    Cart
  },
  data() {
    return {
      isActive: false,
      cartActive: false,
      counter: 0,
    }
  },
  created() {
    eventBus.$on('gamebought', () => this.counter++);
    eventBus.$on('closecart', () => this.cartActive = false)
  },
  methods: {
    showMenu() {
      this.isActive = !this.isActive
    },
    openCart() {
      this.cartActive = true;
    },
    changeIcon() {
      if(this.isActive === false) return require('../assets/icons/icon_hamburguer.png')
      return require('../assets/icons/close icon.png')
    },
  },
}
</script>

<style scoped>

#header {
  background-color: rgba(0, 0, 0, 0);
  width: calc(100% - 20px);

  height: 80px;
  position: absolute;
  z-index: 1000;
  display: flex;
  top:0;
  align-items: center;
  padding: 0px 10px;
  justify-content:space-around;
}

a {
  text-decoration: none;
}

.brand {
  display: flex;
  align-items: center;
}

.brand .logo {
  width: 100px;
}

.dropdown {
  float: left;
  overflow: hidden;
}

.dropdown .dropbtn {
  font-size: 16px;
  border: none;
  outline: none;
  color: white;
  padding: 14px 16px;
  background-color: inherit;
}

.dropdown-content {
  display: none;
  position: absolute;
  border-radius: 5px;
  padding: 20px;
  background-color: #084154;
  min-width: 500px;
  height: 200px;
  border: 2px solid #3EC6E0;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  z-index: 1;
  overflow: hidden;
  box-shadow: 6px 6px 0px #3EC6E0;
}

.dropdown-section {
  display: flex;
  flex-direction: column;
  flex: 1
}

.dropdown-item, .dropdown-title {
  display: inline-block;
  width: 70%;
  border-radius: 5px;
  padding: 8px 16px;
  color: #fff;
  font-size: 14px;
}

.dropdown-title {
  font-size: 16px;
  font-weight: bold;
}

.dropdown-item:hover {
  background-color: #3EC6E0;
  transition: 0.3s;
}

ul {
  display: flex;
  justify-content:space-between;
  padding-left: 0px;
}

li {
  color:white;
  list-style-type: none;
  display: flex;
  align-items: center;
  justify-content: center;
  width: clamp(40px, 15vw, 140px);
  font-size: 14px;
}

ul .border {
  border-right: 2px solid white;
}

.icon {
  width: 20px;
  margin-right: 10px;
}

.icon:hover, li:hover {
  opacity: 0.7;
  transition: 0.2s;
}

.badge {
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

/* Animações de carrinho */

.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .4s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to {
  transform: translateX(400px);
  opacity: 0;
}

/* Exibe menu  */
.active {
  display:flex;
}

/* Responsividade para mobile  */

@media only screen and (max-width: 767px) {
  li span {
      display: none;
  }
  ul .border {
    border: none
  }
  #header {
    justify-content:space-between; 
    width: 100%;
    padding: 0
  }
  .icon {
    margin-right: 0px;
  }
  
  .solidBG {
    background-color: #084154!important;
  }

  .dropdown-content {
    width: calc(100% - 40px);
    min-height: calc(100vh - 50px);
    border: unset;
    border-radius: unset;
    z-index: 1;
    overflow: hidden;
    box-shadow: unset ;
    flex-wrap: wrap;
    min-width: unset;
  }

  .dropdown-section:not(:last-child) {
    border-bottom: 1px solid #062C38;

  }

  .dropdown-section {
    display:flex;
    justify-content: center;
    text-align: left;
    min-width: 100%;
  }

  .dropdown-item, .dropdown-title {
    display: block;
    width: calc(100% - 32px);
    border-radius: 5px;
    padding: 8px 16px;
    color: #fff;
    font-size: 14px;
  }
  .dropdown-title {
    font-size: 16px;
    font-weight: bold;
  }
  .active {
    display:flex;
  }
}
</style>
