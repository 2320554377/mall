<template>
  <div>
    <nav-bar class="home-nav">
        <template #center>
            <span>购物街</span>
        </template>
    </nav-bar>
    <!-- <b-scroll> -->
      <scroll :imgArr="banner" class="scrollUse"></scroll>
      <recommend-view :features="recommend"></recommend-view>
      <feature-view></feature-view>
      <tabControl :tabTitle="['流行', '新款', '精选']" class="tabControlUse" @tabControlClick="switchList"></tabControl>
      <goods-list 
      :goodsList="goods[currentList].list"
      :goodsScroll="goods[currentList].scrollPx"
      :isClicked="goods.isClicked"
      @scrollPosChanged="setScrollPos"
      >
      </goods-list>
    <!-- </b-scroll> -->
    <Pull-for-more @askForMore="forHomeGoods(currentList)"></Pull-for-more>
     <back-top></back-top>
  </div>
</template>

<script>
import navBar from '@/components/common/navbar/navBar.vue'
import scroll from '@/components/common/scroll/scroll.vue'
import tabControl from '@/components/common/tabControl/tabControl.vue'
import goodsList from '@/components/common/goodsList/goodsList.vue'
import backTop from '@/components/common/backTop/backTop.vue'
import PullForMore from '@/components/common/pullForMore/pullForMore.vue'
// import BScroll from '@/components/common/betterScroll/BScroll.vue'

import recommendView from '@/views/home/childCpns/recommendView.vue'
import featureView from '@/views/home/childCpns/featureView.vue'

import {getHomeMultidata, getHomeGoods} from '@/network/home'

export default {
    name: 'home',
    data(){
      return {
        banner: [],
        recommend: [],
        goods: {
          pop: {
            page: 1,
            list:[],
            scrollPx: 0
          },
          new: {
            page: 1,
            list: [],
            scrollPx: 0
          },
          sell: {
            page: 1,
            list: [],
            scrollPx: 0
          },
          isClicked: 0,
          
        },
        currentList: 'pop',
      }
    },
    components: {
    navBar,
    scroll,
    recommendView,
    featureView,
    tabControl,
    goodsList,
    backTop,
    PullForMore
    // BScroll

},
    created(){
      //申请数据
      this.forHomeMultidata();
      this.forHomeGoods('pop');
      this.forHomeGoods('new');
      this.forHomeGoods('sell');
    },
    methods: {
      forHomeMultidata(){
        getHomeMultidata()
        .then(res => {
          this.banner = res.data.data.banner.list;
          this.recommend = res.data.data.recommend.list;
        })
        .catch(err => console.log(err))
      },
      forHomeGoods(type){
        // 复习，type为变量，通过变量调取对象属性要通过中括号，因为点运算符会将其解析为字符串
        let page = this.goods[type].page
        getHomeGoods(type, page)
        .then(res => {
          this.goods[type].list.push(...res.data.data.list);
          this.goods[type].page++;
        })
        .catch(err => console.log(err))
      },
      switchList(currentIndex){
        switch(currentIndex){
          case 0:
            this.currentList = 'pop';
            break;
          case 1:
            this.currentList = 'new';
            break;
          case 2:
            this.currentList = 'sell'
            break;
        }
        //通过毫秒数来实现参数变化，以便goodsList中监听
        this.goods.isClicked = Date.now();
      },
      setScrollPos(scrollpos){
        this.goods[this.currentList].scrollPx = scrollpos
      }
    }
}
</script>

<style>
.home-nav{
    color: #fff;
    background-color: var(--color-tint);
}
.scrollUse{
  margin-top: 44px;
}
.tabControlUse{
  position: sticky;
  top: 44px;
}
*::-webkit-scrollbar{
  display: none;
}
</style>