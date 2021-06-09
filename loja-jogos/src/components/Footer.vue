<template>
  <div id="footer">
    <div class="footer-left">
      <img src="../assets/footer-brand.png" alt="">
    </div>
    <div class="footer-right">
      <span>Agência N1 - Todos os direitos reservados</span>
    </div>
  </div>
</template>

<style scoped>
#footer {
  display: flex;
  flex-direction: row;
  align-items: center;
  height: 40px;
}

.footer-left {
  background-color: #084154;
  display: flex;
  justify-content: flex-end;
  width: 20%;
  height: 40px;
  padding: 0px 10px;
  align-items: center;
}

span {
  font-size: 14px;
  color: rgb(255, 255, 255)
}

.footer-right {
  background-color: #3EC6E0;
  display: flex;
  padding: 0px 10px;
  width: 80%;
  height: 40px;
  align-items: center;
}

@media only screen and (max-width: 767px) {
  .footer-left {
    width: auto
  }
  
.footer-right {
    width: 100%;
  }
}
</style>