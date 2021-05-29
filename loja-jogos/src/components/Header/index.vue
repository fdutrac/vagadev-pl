<template>
  <nav id="header">
    <div class="brand">
      <div class="dropdown">
        <button class="dropbtn"  @click="showBtn">
          <img class="icon" src="../../assets/icons/icon_hamburguer.png">
        </button>
        <div class="dropdown-content" :class="{active: isActive}">
          <a href="#">Link 1</a>
          <a href="#">Link 2</a>
          <a href="#">Link 3</a>
        </div>
      </div>
      <img class="logo" src="../../assets/brand.png" alt="">
    </div>
    <ul>
      <li class="border">
        <img class="icon" src="../../assets/icons/paper-plane.png">
        <span>
        contato
        </span>
      </li>
      <li class="border">
        <img class="icon" src="../../assets/icons/search-solid.png">
        <span>
        buscar
        </span>
      </li>
      <li>
        <img class="icon" src="../../assets/icons/shopping-bag-solid.png">
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'Header',
  props: {
  },
  data() {
    return {
      isActive: false
    }
  },
  methods: {
    showBtn() {
      this.isActive = !this.isActive
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import './Header.css';

</style>
