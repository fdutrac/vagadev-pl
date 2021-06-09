<template>
   <div class="card">
       <img :src="`cards/${game.img}.png`" class="img" alt=""/>
     <div class="card-description">
       <div class="card-description--border">
         ''
       </div>
       <div class="card-title--container"> 
        <span class="card-title">
          {{ game.title }}
        </span>
        <hr />
       </div>
     </div>
   </div>
</template>

<script>

export default {
  name: 'Card',
  props: {
    game: {
      img: '',
      title: ''
    },
  },
}

</script>
<style scoped>
.card-title--container {
  padding: 0px 10px;
  display: flex;
  width: 100%;
  align-items: center;
  justify-content: space-between;
  color: #084154;
  font-weight: 700;
}

.card-title {
  flex: 4;
}

.card-title--container hr {
  flex: auto;
  width: 20%;
  align-self: center;
  justify-self: end;
  border: none;
  background-color: #084154;
  height: 1px;
}

.card-description {
  height: 50px;
  display:flex;
  align-items: center;
  background-color: #3EC6E0;
  border-radius: 0px 0px 10px 10px;
  margin-top: -4px;
  overflow: hidden;
}

.card-description--border {
  display:flex;
  align-items: center;
  background-color: #084154;
  height: 100%;
  color: rgba(0, 0, 0, 0);
  width: clamp(5px, 2vw, 11px);
}

.card {
  max-width: 500px;
  min-height: auto;
  padding: 10px;
}

.img {
  max-width: 100%;
  height: auto ;
}
</style>