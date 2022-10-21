<template>
  <div>
    <div class="wrapper" ref="scroll">
        <div class="content">
            <slot></slot>
        </div>
    </div>
  </div>
</template>

<script>
import BScroll from "@better-scroll/core"
import Pullup from '@better-scroll/pull-up'

BScroll.use(Pullup);

export default {
    name: 'scroll',
    data(){
        return {
            scroll: null
        }
    },
    methods: {
        
    },
    mounted(){
        this.scroll = new BScroll(this.$refs.scroll, {
            click: true,
            probeType: 3,
            // bounce: true,
            pullUpLoad: true,
            // scrollY: true,
            // disableTouch: false,
        })
        this.scroll.on('pullingUp', ()=>{
            console.log(111);
        })
        document.getElementsByTagName('img').onload = function(){
            this.scroll.refresh()
        }
    }
}
</script>

<style scoped>
.wrapper{
    height: 100vh;
    overflow: hidden;
}
</style>