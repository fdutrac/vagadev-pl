<template>
  <div>
    <transition name="fade">
      <div v-if="isActive" class="slider-content content-1">

      </div> 
      <div v-if="!isActive" class="slider-content content-2">
      </div>
    </transition>
    <div class="slider-navigation">
      <div class="slider-title">
        {{ selectedItem.title }}
      </div>
      <div class="slider-buttons">
        <span>{{ selectedItem.order }} / 2</span>
        <button @click="changeContent('red-dead')">
          <img src="../../assets/icons/angle-left-solid.png" alt="">
        </button>
        <button @click="changeContent('mortal-kombat')">
          <img src="../../assets/icons/angle-right-solid.png" alt="">
        </button>
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
        selectedItem: {
          title: 'MORTAL KOMBAT',
          order: '1',
          description: 'Mortal Kombat X combina uma apresentação cinemática única com uma jogabilidade totalmente nova. Os jogadores podem escolher pela primeira vez diversas variantes de cada personagem, afetando tanto a estratégia como o estilo de luta.'
        },
        games: {
          game1:{
            title: 'MORTAL KOMBAT',
            order: '1',
            description: 'Mortal Kombat X combina uma apresentação cinemática única com uma jogabilidade totalmente nova. Os jogadores podem escolher pela primeira vez diversas variantes de cada personagem, afetando tanto a estratégia como o estilo de luta.' 
          },
          game2: {
            title: 'RED DEAD REDEMPTION II',
            order: '2',
            description: 'Mortal Kombat X combina uma apresentação cinemática única com uma jogabilidade totalmente nova. Os jogadores podem escolher pela primeira vez diversas variantes de cada personagem, afetando tanto a estratégia como o estilo de luta.' 
          },
        }
      }
    },
  methods: {
    changeContent(selected) {
      if (selected === 'red-dead') {
        this.isActive = true
        this.selectedItem.title = this.games.game1.title;
        this.selectedItem.order = this.games.game1.order;
      } else if (selected === 'mortal-kombat') {
        this.isActive = false
        this.selectedItem.title = this.games.game2.title;
        this.selectedItem.order = this.games.game2.order;
      }
    }
  }
}

</script>
<style>


.slider-content{
  height: max(40vw, 400px);
}

.slider-title {
  padding: 0px 10px
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
  transition: 0.5s;
  transition: all 0.3s linear;
  background-image: url('../../assets/carousel/principal_banner_desktop 1.png');
  background-size:cover;
}
.content-2 {
  transition: 0.5s;
  transition: all 0.3s linear;
  background-image: url('../../assets/carousel/principal_banner_desktop_02.png');
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


</style>