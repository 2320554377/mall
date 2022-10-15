<template>
  <div>
    <nav-bar class="home-nav">
        <template #center>
            <span>购物街</span>
        </template>
    </nav-bar>
    <scroll :imgArr="banner" class="scrollUse"></scroll>
    <recommend-view :features="recommend"></recommend-view>
    <featureView></featureView>
    <tabControl :tabTitle="['流行', '新款', '精选']" class="tabControlUse"></tabControl>
    <ul>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li><li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li><li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li><li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li><li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li><li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li><li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
      <li>foo</li>
    </ul>
  </div>
</template>

<script>
import navBar from '@/components/common/navbar/navBar.vue'
import scroll from '@/components/common/scroll/scroll.vue'
import tabControl from '@/components/common/tabControl/tabControl.vue'

import recommendView from '@/views/home/childCpns/recommendView.vue'
import featureView from '@/views/home/childCpns/featureView.vue'

import {getHomeMultidata} from '@/network/home'

export default {
    name: 'home',
    data(){
      return {
        banner: [],
        recommend: []
      }
    },
    components: {
        navBar,
        scroll,
        recommendView,
        featureView,
        tabControl
    },
    created(){
      getHomeMultidata()
      .then(res => {
        this.banner = res.data.data.banner.list;
        this.recommend = res.data.data.recommend.list;
      })
      .catch(err => console.log(err))
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
</style>