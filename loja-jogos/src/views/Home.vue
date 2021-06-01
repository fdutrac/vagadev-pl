<template>
  <div>
    <Slider />
    <div class="cards-container">
      <Card :game="games.game1"/>
      <Card :game="games.game2"/>
    </div>
    <div class="spotlights">
      <div class="spotlights-nav--left" @click="selectPrevious" :class="selected === 1 ? 'unclickable' : ''">
        <img src="../assets/icons/angle-left-solid.png" class="spotlight-nav--img" alt="">
      </div>
      <div class="spotlights-container">
        <Spotlight class="spotlight" :class="selected === 1 ? selected : 'notSelected'" :game="spotlights[0]"/>
        <Spotlight class="spotlight" :class="selected === 2 ? selected : 'notSelected'" :game="spotlights[1]"/>
        <Spotlight class="spotlight" :class="selected === 3 ? selected : 'notSelected'" :game="spotlights[2]"/>
      </div>
      <div class="spotlights-nav--right" @click="selectNext">
        <img src="../assets/icons/angle-right-solid.png" class="spotlight-nav--img" :class="selected === 3 ? 'unclickable' : ''" alt="">
      </div>
    </div>
  </div>
  
</template>

<script>
// @ is an alias to /src
import Slider from '@/components/Slider.vue';
import Card from '@/components/Card.vue';
import Spotlight from '@/components/Spotlight.vue';
import products from '../../product-storage.json';

export default {
  name: 'Home',
  components: {
    Slider,
    Card,
    Spotlight
  },
  data() {
    return {
      selected: 1,
      games: {
        game1: {
          title: 'The Legend of Zelda - Breath of the wild',
          img: 'zelda_banner'
        },
        game2: {
          title: 'SEKIRO - Shadows die twice',
          img: 'sekiro_banner'
        },
      },
      spotlights: products
    }
  },
  methods: {
    selectNext() {
      if (this.selected < 3) {
        this.selected++
      }
    },
    selectPrevious() {
      if (this.selected > 1) {
        this.selected--
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

.spotlights-container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
.spotlights {
  position: relative;
}

.spotlights-nav--left, .spotlights-nav--right {
  display: none;
  position: absolute;
  top: 50%
}
.spotlights-nav--left {
  left: 10%;
}
.spotlights-nav--right {
  right: 10%;
}

.spotlight-nav--img {
  filter: invert(100%);
  height: 25px
}
.unclickable {
  filter: invert(50%)!important;
}


@media only screen and (min-width: 1024px) {
  .cards-container {
    margin-top: -5%;
    position: relative;
  }
}

@media only screen and (max-width: 767px) {
  .spotlights-nav--left, .spotlights-nav--right {
    display: block;
  }
  .selected {
    display: block
  }
  .notSelected {
    display: none!important;
  }
}
</style>