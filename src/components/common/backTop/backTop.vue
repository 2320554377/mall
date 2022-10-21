<template>
    <div id="backTop" class="noshow" @click="clickcpn">
      <img src="@/assets/img/common/top.png" alt="">
    </div>
  </template>
  
  <script>
  export default {
      name: 'backTop',
      data(){
          return {
              scrollTop: 0,
              beforeHeight: 1,
              isShowBoolen: false
          }
      },
      mounted(){
          //
          window.onscroll = function(){
              this.scrollTop = window.pageYOffset || document.body.scrollTop || document.documentElement.scrollTop
              this.beforeHeight = 
                  document.getElementsByClassName('home-nav')[0].offsetHeight + 
                  document.getElementsByClassName('scrollUse')[0].offsetHeight +
                  document.getElementsByClassName('featureView')[0].offsetHeight +
                  document.getElementsByClassName('featureView')[1].offsetHeight - 44;
              if(this.scrollTop < this.beforeHeight){
                  document.getElementById('backTop').setAttribute('class','noshow')
              }else{
                  document.getElementById('backTop').setAttribute('class','')
              }
          }
      },
      methods: {
          clickcpn(){
              //点击跳转回顶部
              // document.body.scrollTop = 0
              // document.documentElement.scrollTop = 0
              window.scrollTo({
                  top: 0,
                  behavior: 'smooth'
              });
          }
      }
  }
  </script>
  
  <style>
  #backTop{
      position: fixed;
      right: 0;
      bottom: 40px;
  }
  .noshow{
      display: none;
  }
  </style>