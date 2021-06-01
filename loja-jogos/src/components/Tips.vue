<template>
   <div class="card">
      <div class="card-sequence">
        {{sequence}}
      </div>
      <img :src="game.thumbnail" class="card-img" alt=""/>
   </div>
</template>

<script>

export default {
  name: 'Tips',
  props: {
    game: {
    },
    sequence: Number
  },
}

</script>
<style scoped>



.card {
  position:relative;
  max-width: 220px;
  min-height: auto;
  margin: 10px;
  margin-top: 25px; 
}
.card-sequence {
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  top:-25px;
  right: 5%;
  width: 50px;
  height: 50px;
  color: white;
  background-color: #3EC6E0;
  border: 2px solid #084154;
  border-radius: 5px;
  font-size: 36px;
  -webkit-text-stroke-width: 1px;
  -webkit-text-stroke-color: #084154;
}

.card-img {
  max-width: 100%;
  height: auto;
}

@media only screen and (max-width: 767px) {
  .card {
    max-width: 100%;
  }
}
@media only screen and (min-width: 1367px) {
  .card {
    max-width: 300px;
  }
}
</style>