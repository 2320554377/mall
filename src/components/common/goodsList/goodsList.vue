<template>
    <div class="goodsList">
      <goods-list-item v-for="item in goodsList" :key="getSymbol(item.title)">
          <template #goodsImg>
              <img :src="item.show.img" alt="">
          </template>
          <template #goodsInfo>
              <p>{{item.title}}</p>
              <span class="price"><b>￥{{item.price}}</b></span>
              <span class="orgPrice"><s>{{item.orgPrice}}</s></span>
              <p class="sale">已售{{item.sale}}</p>
          </template>
      </goods-list-item>
    </div>
  </template>
  
  <script>
  import goodsListItem from './goodsListItem.vue'
  export default {
      name: 'goodsList',
      data(){
          return {
              localScrollpos: 0,
          }
      },
      props: {
          goodsList: {
              type: Array,
              default(){
                  return []
              }
          },
          goodsScroll: {
              type: Number,
              default:0
          },
          isClicked: {
              type: Number,
              default: 0
          },
      },
      components: {
          goodsListItem
      },
      watch: {
          //监听isClicked
          isClicked(newVal){
              newVal && this.onChanged()
          },
          goodsScroll(newVal){
              this.localScrollpos = newVal
          }
      },
      methods: {
          getSymbol(type){
              return Symbol(type)
          },
          onChanged(){
                  if(this.goodsScroll === 0){
                      this.localScrollpos = 
                          (document.getElementsByClassName('home-nav')[0].offsetHeight + 
                          document.getElementsByClassName('scrollUse')[0].offsetHeight +
                          document.getElementsByClassName('featureView')[0].offsetHeight +
                          document.getElementsByClassName('featureView')[1].offsetHeight - 44)
                          window.scrollTo(0,this.localScrollpos)
                  }else{
                      window.scrollTo(0,this.goodsScroll)
                  }
                  let that = this
                  window.addEventListener('scroll', ()=>{
                      that.localScrollpos = window.scrollTop
                      that.$emit('scrollPosChanged', that.localScrollpos)
                  })
              }
          },
          mounted(){
              //解决浏览默认list时候无法记录滚动位置的问题
              let that = this
              window.addEventListener('scroll', ()=>{
                      if(!that.isClicked){
                          that.localScrollpos = window.scrollTop
                          that.$emit('scrollPosChanged', that.localScrollpos)
                      }
                  })
          }
  }
  </script>
  
  <style>
  .goodsList{
      display: flex;
      flex-wrap: wrap;
      justify-content: space-evenly;
  }
  .goods{
      width: 46vw;
      padding-bottom: 10px;
  }
  .goodsImg img{
      width: 46vw;
      border-radius: 5px;
  }
  .goodsInfo p{
      /* 超出显示点点点 */
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      padding: 5px 0;
  }
  .price{
      color: var(--color-tint);
  }
  .sale, .orgPrice{
      font-size: 15px;
  }
  </style>