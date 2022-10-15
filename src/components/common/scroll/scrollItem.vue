<template>
  <div class="scrollItem">
    <slot></slot>
  </div>
</template>

<script>
export default {
    name: 'scrollItem'
}
</script>

<style>
    .scrollItem{
        /* float: left; */
        overflow: hidden;
        flex-shrink: 0;
    }
    .scrollItem img{
      /* 一个vw表示1%视口宽度 */
        width: 100vw;
    }
</style>