<template>
  <div class="goods">
    <div class="goodsImg"><slot name="goodsImg"></slot></div>
    <div class="goodsInfo"><slot name="goodsInfo"></slot></div>
  </div>
</template>

<script>
export default {
    name: 'goodListItem'
}
</script>

<style>

</style>