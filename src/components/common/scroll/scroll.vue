<template>
  <div id="scrollContainer">
    <div id="scrollShell" v-on="{touchstart:onTouch,touchend:onTouchOver,touchmove:onTouchMove}">
        <scrollItem v-for="item in imgArr" :key="item.title">
            <!-- 注意img的src要用v-bind进行绑定！ -->
            <a :href="item.link"><img :src="item.image" alt="" srcset=""></a>
        </scrollItem>
    </div>
    <ul class="bottomItems">
        <li v-for="(item, index) in imgArr" :key="item.title" :class="{current:currentIndex == index + 1}"></li>
    </ul>
  </div>
</template>

<script>
import scrollItem from './scrollItem.vue'
export default {
    name: 'scroll',
    data(){
        return {
            currentIndex: 1,
            timer: null,
            timerNum:0,
            touchStart:{
                x: 0,
                y: 0
            }
        }
    },
    methods:{
        handleDom(){
            // 处理dom，为第一张前和最后一张后插入最后一张和第一张图片，保证平滑切换
            if(this.imgArr.length > 1){
                let scrollShell = document.getElementById('scrollShell');
                let scrollItem = document.getElementsByClassName('scrollItem');
                //插入节点操作
                let first = scrollItem[0].cloneNode(true);
                let last = scrollItem[this.imgArr.length - 1].cloneNode(true);
                scrollShell.insertBefore(last, scrollItem[0]);
                scrollShell.appendChild(first);
                //处理完dom之后将偏移量滚动到第二个图片
                this.scroll();
            }
        },
        /**
         * 通过translateX实现shell滚动
         */
        scroll(){
            document.getElementById('scrollShell').style.transform = `translateX(${-this.currentIndex * 100}vw)`
        },
        /**
         * 检查当前显示图片的序号，确保其不越界，并实现首位跳转
         */
        check(){
            document.getElementById('scrollShell').setAttribute('class','transitionStyle');
            if(this.currentIndex === this.imgArr.length + 1){
                this.scroll();
                //放计时器使最后一张图片向后滚动时，不会因为noneTransitionStyle类的添加而使过渡效果消失
                setTimeout(()=>{
                    document.getElementById('scrollShell').setAttribute('class','noneTransitionStyle')
                    this.currentIndex = 1;
                    this.scroll();
                },200)
            }else if(this.currentIndex === 0){
                this.scroll();
                setTimeout(()=>{
                    document.getElementById('scrollShell').setAttribute('class','noneTransitionStyle')
                    this.currentIndex = this.imgArr.length;
                    this.scroll()
                },200)
            }
        },
        next(){
            this.currentIndex++;
            this.check();
            this.scroll();
        },
        before(){
            this.currentIndex--;
            this.check();
            this.scroll();
        },
        setTimer(){
            this.timer = window.setInterval(()=>{
                document.getElementById('scrollShell').setAttribute('class','transitionStyle');
                this.next();
            }
            ,3000);
            //通过$once监听来使timer失效，具体看笔记
            this.$once('hook:beforeDestroy', () => {
                window.clearInterval(this.timer);
            })
        },
        clearTimer(){
            window.clearInterval(this.timer);
            this.timer = null;
        },
        //触摸时调用
        onTouch(e){
            this.clearTimer();
            //获取起点坐标信息
            this.touchStart = {
                x: e.changedTouches[0].pageX,
                y: e.changedTouches[0].pageY
            }
        },
        //触摸点移动时调用
        onTouchMove(e){
            this.clearTimer();
            //换算移动距离为vw单位
            let vw = (-this.currentIndex + (e.changedTouches[0].pageX-this.touchStart.x)/document.getElementsByClassName('scrollItem')[0].offsetWidth)*100
            document.getElementById('scrollShell').style.transform = `translateX(${vw}vw)`
            //阻止冒泡，防止触摸点移动时父容器也移动
            e.preventDefault();
        },
        //触摸抬起调用
        onTouchOver(e){
            let dx = e.changedTouches[0].pageX - this.touchStart.x;
            let width = document.getElementsByClassName('scrollItem')[0].offsetWidth;
            if(dx < 0&&Math.abs(dx/width) > 0.3){
                this.next();
            }else if(dx > 0&&dx/width>0.3){
                this.before();
            }else{
                this.scroll();
            }
            if(this.timer === null){
                this.setTimer();
            }
        }
    },
    props: {
        imgArr:{
            type: Array,
            default(){
                return []
            }
        }
    },
    mounted: function () {
      setTimeout(() => {
        this.handleDom();
        if(this.timer === null){
            this.setTimer();
        }
      }, 1000)
    },
    components: {
        scrollItem
    },
}
</script>

<style>
    #scrollContainer{
        position: relative;
        overflow-x: hidden;
    }
    #scrollShell{
        display: flex;
    }
    .bottomItems{
        position: absolute;
        bottom: 10px;
        left: 50%;
        transform: translateX(-50%);
    }
    .bottomItems li{
        float: left;
        margin: 0 5px;
        height: 10px;
        width: 10px;
        border: 1px solid #ccc;
        border-radius: 10px;
    }
    .current {
        background-color: #ccc;
    }
    .transitionStyle{
        transition: .2s;
    }
    .noneTransitionStyle{
        transition: 0;
    }
</style>