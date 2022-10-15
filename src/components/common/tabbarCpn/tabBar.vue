<template>
  <div id="tab-bar">
    <slot></slot>
    </div>
</template>

<script>
export default {
    name: 'tabBar'
}
</script>

<style>
#tab-bar{
  position: fixed;
  display: flex;
  height: 49px;
  padding: 5px 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #f6f6f6;
  box-shadow: 0px -1px 1px rgba(100, 100, 100, .2);
}
.tab-bar-item {
  flex: 1;
  text-align: center;
  font-size: 15px;
}
.tab-bar-item img{
  width: 20px;
}
</style>