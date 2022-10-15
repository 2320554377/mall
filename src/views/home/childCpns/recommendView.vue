<template>
    <div class="featureView">
      <div class="featureItem" v-for="item in features" :key="item.title">
          <a :href="item.link">
              <img :src="item.image" alt="" srcset="">
              <span>{{item.title}}</span>
          </a>
      </div>
    </div>
  </template>
  
  <script>
  export default {
      name: 'recommendView',
      props: {
          features: {
              type: Array,
              default(){
                  return []
              }
          }
      }
  }
  </script>
  
  <style>
  .featureView{
      display: flex;
      width: 100vw;
      overflow: hidden;
      padding: 15px 0 30px;
      border-bottom: 8px solid #eee;
  }
  .featureItem{
      text-align: center;
      /* width: 100%; */
      flex: 1;
  }
  .featureItem img{
      width: 16vw;
      padding: 0 2vw;
  }
  .featureItem span{
      font-size: 5vw;
      display: block;
  }
  </style>