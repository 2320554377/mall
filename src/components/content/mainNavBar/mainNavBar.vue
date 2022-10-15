<template>
  <div>
    <nav-bar class="home-nav">
        <template #center>
            <span>购物街</span>
        </template>
    </nav-bar>
  </div>
</template>

<script>
import navBar from '@/components/common/navbar/navBar.vue'
import navBarItem from '@/components/common/navbar/navBarItem.vue'

export default {
    name: 'mainNavBar',
    components: {
        navBar,
        navBarItem
    }
}
</script>

<style>
.home-nav{
    background-color: var(--color-tint);
}
</style>