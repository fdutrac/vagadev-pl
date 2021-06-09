<template>
  <div class="slider">
    <transition name="slide" type="animation">
      <div v-if="isActive" class="slider-content content-1">
        <div class="slider-description game-one">
          <h1>{{ games.game1.title}}</h1>
          <h2>{{ games.game1.value}}</h2>
          <p>{{ games.game1.description}}</p>
        </div>
      </div>
      <div v-if="!isActive" class="slider-content content-2">
        <div class="slider-description game-two">
          <h1>{{ games.game2.title}}</h1>
          <h2>{{ games.game2.value}}</h2>
          <p>{{ games.game2.description}}</p>
        </div>
      </div>
    </transition>
    <div class="slider-navigation">
      <div class="slider-title">
        <span>
          {{ selectedItem.title }}
        </span>
        <hr/>
      </div>
      <div class="slider-buttons">
        <div class="slider-counter">
          <span>{{ selectedItem.order }} / 2</span>
        </div>
        <div class="slider-button--container">
          <button @click="changeContent('red-dead')">
            <img src="../assets/icons/angle-left-solid.png" alt="">
          </button>
          <button @click="changeContent('mortal-kombat')">
            <img src="../assets/icons/angle-right-solid.png" alt="">
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Carousel',
  components: {  },
  data() {
    return {
        isActive: true,
        selectedItem:
        {
          title: 'MORTAL KOMBAT',
          order: '1',
          description: 'Mortal Kombat X combina uma apresentação cinemática única com uma jogabilidade totalmente nova. Os jogadores podem escolher pela primeira vez diversas variantes de cada personagem, afetando tanto a estratégia como o estilo de luta.'
        },
        games: {
          game1:{
            title: 'MORTAL KOMBAT',
            order: '1',
            value: 'R$299,99',
            description: 'Mortal Kombat X combina uma apresentação cinemática única com uma jogabilidade totalmente nova. Os jogadores podem escolher pela primeira vez diversas variantes de cada personagem, afetando tanto a estratégia como o estilo de luta.'
          },
          game2: {
            title: 'RED DEAD REDEMPTION II',
            order: '2',
            value: 'R$249,99',
            description: 'Em 1899, Red Dead Redemption 2 segue a história de Arthur Morgan, um membro da guangue de bandidos de Dutch Van der Linde. Com agentes federais e os melhores caçadores de recompensa em seu encalço, a gangue precisa roubar, assaltar e lutar para sobreviver no impiedoso coração dos Estados Unidos.'
          },
        }
      }
    },
  methods: {
    changeContent(selected) {
      if (selected === 'red-dead') {
        this.isActive = true
        this.selectedItem = this.games.game1;
      } else if (selected === 'mortal-kombat') {
        this.isActive = false
        this.selectedItem = this.games.game2;
      }
    }
  },
  created() {
    setInterval(() => {
      if (this.isActive === false) {
        this.isActive = true
        this.selectedItem = this.games.game1;
      } else if (this.isActive === true) {
        this.isActive = false
        this.selectedItem = this.games.game2; }
      }, 5000
    );
  }
}

</script>
<style scoped>
h1, h2 {
  margin: 0
}
h1 {
  font-size: clamp(1.5rem, 3vw, 3rem);
}
h2 {
  font-size: clamp(3rem, 6vw, 4.5rem);
}
p {
  font-size: clamp(0.8rem, 2vw, 1rem);
}

.slider-content{
  position:relative;
  height: max(40vw, 400px);
}

.slider-title {
  padding: 0px 10px
}

.slider-title hr {
  display: none;
}

.slider-description {
  text-align: end;
  display: block;
  position: absolute;
  bottom: 0;
  width: calc(100% - 60px);
  margin-top: auto;
  background: rgba(0,0,0,0.65);
  padding: 30px;
}

.slider-description h1, p {
  color: white;
}

.slider-description h2 {
  color: #3EC6E0;
}

.slider-navigation {
  height: 50px;
  display:flex;
  align-items: center;
  justify-content:space-between;
  background-color: #3EC6E0;
  border-bottom-left-radius: 10px;
  color: white;
  font-size: 14px;
}

.slider-buttons{
  display: inherit;
  align-items: inherit;
  right: 0;
  justify-content: space-evenly;
  height: 100%;
  width: 120px;
  background-color: #084154;
}

.slider-buttons button {
  border: none;
  background-color: inherit;
}

.content-1 {
  transition: 1s;
  background-image: url('../assets/carousel/principal_banner_desktop 1.png');
  background-size:cover;
}

.content-2 {
  transition: 1s;
  background-image: url('../assets/carousel/principal_banner_desktop_02.png');
  background-size: cover;
}

@media only screen and (max-width: 767px) {
  .content-1 {
    background-position: 20%;
  }

  .content-2 {
    background-position: 75%;
  }
}
@media only screen and (min-width: 768px) {
  .game-one {
    right: 20%;
  }

  .game-two {
    left: 10%;
    background-color: rgba(0,0,0,0.65);
    border-radius: 10px;
    max-height: 380px;
    bottom:auto
  }

  .slider-description{
    position: absolute;
    top: 20%;
    max-width: 420px;
    background-color: inherit
  }

  .slider-navigation {
    height: 50px;
    display:flex;
    position: absolute;
    right: -122px;
    top: 33%;
    -webkit-transform: rotate(90deg);
    -moz-transform: rotate(90deg);
    -o-transform: rotate(90deg);
    -ms-transform: rotate(90deg);
    transform: rotate(90deg);
    align-items: center;
    justify-content:space-between;
    background-color: #3EC6E0;
    border-bottom-left-radius: 0px;
    overflow: hidden;
    border-bottom-right-radius: 10px;
    color: white;
    font-size: 14px;
  }

  .slider-buttons {
    width: auto
  }

  .slider-title {
    width: 200px;
    display: flex
  }

  .slider-button--container, .slider-counter {
    transform: rotate(-90deg);
  }

  .slider-title hr {
    width: 30%;
    align-self: center;
    display:block;
    border: none;
    background-color: rgb(255, 255, 255);
    color: rgb(255, 255, 255);
    height: 1px;
  }
}


</style>