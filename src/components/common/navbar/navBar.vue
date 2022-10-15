<template>
  <div class="nav-bar">
    <div class="left"><slot name="left"></slot></div>
    <div class="nav-bar-center"><slot name="center"></slot></div>
    <div class="right"><slot name="right"></slot></div>
  </div>
</template>

<script>
export default {

}
</script>

<style>
.nav-bar{
    height: 44px;
    display: flex;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    box-shadow: 0px 1px 1px rgba(100, 100, 100, .2);
    line-height: 44px;
    font-weight: 500;
    z-index: 99;
}
.nav-bar-center{
    text-align: center;
    flex: 1;
}
.left , .right{
    width: 60px;
}
</style>