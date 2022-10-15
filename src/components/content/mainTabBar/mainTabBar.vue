<template>
  <tab-bar>
      <tab-bar-item path="/home" activeColor="rgb(255,71,109)">
        <template v-slot:icon><img src="~@/assets/img/tabbar/home.svg" alt="" srcset=""/></template>
        <template v-slot:active-icon><img src="~@/assets/img/tabbar/home_active.svg" alt="" srcset=""/></template>
        <template v-slot:text><div>首页</div></template>
      </tab-bar-item>
      <tab-bar-item path="/category" activeColor="rgb(255,71,109)">
        <template v-slot:icon><img src="~@/assets/img/tabbar/category.svg" alt="" srcset=""/></template>
        <template v-slot:active-icon><img src="~@/assets/img/tabbar/category_active.svg" alt="" srcset=""/></template>
        <template v-slot:text><div>分类</div></template>
      </tab-bar-item>
      <tab-bar-item path="/cart" activeColor="rgb(255,71,109)">
        <template v-slot:icon><img src="~@/assets/img/tabbar/cart.svg" alt="" srcset=""/></template>
        <template v-slot:active-icon><img src="~@/assets/img/tabbar/cart_active.svg" alt="" srcset=""/></template>
        <template v-slot:text><div>购物车</div></template>
      </tab-bar-item>
      <tab-bar-item path="/profile" activeColor="rgb(255,71,109)">
        <template v-slot:icon><img src="~@/assets/img/tabbar/profile.svg" alt="" srcset=""/></template>
        <template v-slot:active-icon><img src="~@/assets/img/tabbar/profile_active.svg" alt="" srcset=""/></template>
        <template v-slot:text><div>我的</div></template>
      </tab-bar-item>
    </tab-bar>
</template>

<script>
import tabBar from '@/components/common/tabbarCpn/tabBar.vue'
import tabBarItem from '@/components/common/tabbarCpn/tabBarItem.vue'

export default {
    name: 'mainTabBar',
    components: {
        tabBar,
        tabBarItem
    }
}
</script>

<style>

</style>