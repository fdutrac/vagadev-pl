<template>
  <div>
    <Slider />
    <div class="cards-container">
      <Card :game="games.game1"/>
      <Card :game="games.game2"/>
    </div>
    <section class="spotlights">
      <div class="title-container">
        <img src="../assets/icons/dots-icon.png" class="" alt="">
        <h3>
          Produtos em destaque
        </h3>
      </div>
      <div class="spotlights-nav--left" @click="selectPrevious" :class="selected === 1 ? 'unclickable' : ''">
        <img src="../assets/icons/angle-left-solid.png" class="spotlight-nav--img" alt="">
      </div>
      <div class="spotlights-container">
        <!-- <transition-group name="slide"> -->
          <Spotlight class="spotlight" :class="selected === 1 ? 'selected' : 'notSelected'" :game="spotlights[0]"/>
          <Spotlight class="spotlight" :class="selected === 2 ? 'selected' : 'notSelected'" :game="spotlights[1]"/>
          <Spotlight class="spotlight" :class="selected === 3 ? 'selected' : 'notSelected'" :game="spotlights[2]"/>
        <!-- </transition-group> -->
      </div>
      <div class="spotlights-nav--right" @click="selectNext">
        <img src="../assets/icons/angle-right-solid.png" class="spotlight-nav--img" :class="selected === 3 ? 'unclickable' : ''" alt="">
      </div>
    </section>
    <section class="tips">
      <div class="title-container">
        <img src="../assets/icons/dots-icon.png" class="" alt="">
        <h3>
          Dicas de Games
        </h3>
        <select @change="getCategory(tips.category)" v-model="tips.category" name="tips" id="categories">
          <option value="" disabled selected>Selecione a categoria</option>
          <option value="mmorpg">MMORPG</option>
          <option value="shooter ">Shooter</option>
          <option value="pvp ">PVP</option>
        </select>
      </div>
      <div class="tips-container">
        <Tips v-for="(tip, index) in tips.list" :key="tip.id" :game="tip" :sequence="index+1"/>
      </div>
    </section>
  </div>
  
</template>

<script>
// @ is an alias to /src
import Slider from '@/components/Slider.vue';
import Card from '@/components/Card.vue';
import Spotlight from '@/components/Spotlight.vue';
import Tips from '@/components/Tips.vue';
import products from '../../product-storage.json';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Slider,
    Card,
    Spotlight,
    Tips
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
      tips: {
        category: 'mmorpg',
        list: [],
      },
      spotlights: products
    }
  },
  created() {
    this.getCategory(this.tips.category)
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
    },
    getCategory(category) {
      const options = {
        method: 'GET',
        url: 'https://free-to-play-games-database.p.rapidapi.com/api/games',
        params: {category: category},
        headers: {
          'x-rapidapi-key': '7a0a0eb733msh6b120795a38e22fp196f7fjsn9b18ff081134',
          'x-rapidapi-host': 'free-to-play-games-database.p.rapidapi.com'
        }
      }
      axios.request(options).then(res => (
        this.tips.list = res.data.slice(0, 4)
      ));
    }
  }
}
</script>

<style scoped>
h3 {
  font-weight: 300;
  font-size: clamp(22px, 2vw, 40px);
  color: #084154
}

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

.title-container {
  display: flex;
  margin: auto;
  justify-content: flex-start;
  width:75%;
  align-items: center;
}
.title-container img {
  height: 100%;
  margin-right: 15px;
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
  left: 7%;
}
.spotlights-nav--right {
  right: 7%;
}

.spotlight-nav--img {
  filter: invert(100%);
  height: 25px
}

.unclickable {
  filter: invert(50%)!important;
}

#categories {
  margin-left: 30px;
  padding: 7px;
  border-radius: 5px;
  border-color: #084154;
  font-size: 14px;
  font-weight: 300;
}

.tips-container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  width:80%;
  margin: auto;
  margin-top: 15px;
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
    opacity: 1;
    height: auto;
    transition: 1s ease;
  }
  .notSelected {
    opacity: 0;
    height: 0;
    overflow: hidden;
    margin: 0;
    transform: translateX(-100px);
    transition: 0.5s ease;
  }
  .title-container {
    width:90%;
  }

  .tips .title-container {
    flex-wrap: wrap;
  }
  .tips-container {
  width: 95%;
  }
  #categories {
    width:100%;
    margin-left: 0;
    margin-bottom: 20px;
  }
}
</style>