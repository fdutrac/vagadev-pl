<template>
  <div>
    <Carousel />
    <div class="cards-container">
      <Card :game="games.game1"/>
      <Card :game="games.game2"/>
    </div>
  </div>
  
</template>

<script>
// @ is an alias to /src
import Carousel from '@/components/Slider'
import Card from '@/components/Card'

export default {
  name: 'Home',
  components: {
    Carousel,
    Card
  },
  data() {
    return {
      games: {
        game1: {
          title: 'The Legend of Zelda - Breath of the wild',
          img: 'zelda_banner'
        },
        game2: {
          title: 'SEKIRO - Shadows die twice',
          img: 'sekiro_banner'
        },
      }
    }
  }
}
</script>

<style scoped>
.cards-container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}


@media only screen and (min-width: 1024px) {
  .cards-container {
    margin-top: -5%;
    position: relative;
  }
}
</style>