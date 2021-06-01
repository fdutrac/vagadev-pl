<template>
  <nav id="header">
    <div class="brand">
      <div class="dropdown">
        <button class="dropbtn" @click="showMenu">
          <img class="icon" src="../assets/icons/icon_hamburguer.png">
        </button>
        <div class="dropdown-content" :class="{active: isActive}">
          <a href="#">Link 1</a>
          <a href="#">Link 2</a>
          <a href="#">Link 3</a>
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
      <li>
        <img class="icon" src="../assets/icons/shopping-bag-solid.png">
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
    showMenu() {
      this.isActive = !this.isActive
    }
  }
}
</script>

<style scoped>
#header {
    background-color: rgba(0, 0, 0, 0);
    width: calc(100% - 20px);
    height: 80px;
    position: absolute;
    display: flex;
    top:0;
    align-items: center;
    padding: 0px 10px;
    justify-content:space-around;
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
 .icon:hover, li:hover {
  opacity: 0.7;
  transition: 0.2s;

}

.dropdown-content {
    display: none;
    position: absolute;
    border-radius: 5px;
    background-color: #EBEBEB;
    min-width: 400px;
    box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
    z-index: 1;
    overflow: hidden;
}

.dropdown-content a {
    float: none;
    color: black;
    padding: 12px 16px;
    text-decoration: none;
    display: block;
    text-align: left;
    transition: 0.5s;
}

.dropdown-content a:hover {
    background-color: #ddd;
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

/* Exibe menu  */

.active {
    display: block
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
    }
    .icon {
        margin-right: 0px;
    }
}
</style>
