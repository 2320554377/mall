<template>
  <div class="pullForMore" ref="pullForMore">
    <slot></slot>
  </div>
</template>

<script>

export default {
    name: 'pullForMore',
    props:{
        type: {
            type: String,
            default: ''
        }
    },
    data(){
        return {
            isRequesting: false
        }
    },
    methods: {
        forMore(){
            return this.$emit('askForMore')
        }
    },
    mounted(){
        let that = this
        setInterval(window.addEventListener('scroll', ()=>{
            //内容可视区域的高度
            let clientHeight = document.body.clientHeight
            // 获取页面滚动的距离
            let scrollTop = window.scrollTop
            //屏幕高度
            let screenHeight = window.screen.height
            if(scrollTop + screenHeight >= clientHeight && !that.isRequesting){
                that.forMore();
                that.isRequesting = true;
                setTimeout(that.isRequesting=false, 1000);
            }
        }),300)
    }
}
</script>

<style>
.pullForMore{
    overflow: auto;
}
</style>