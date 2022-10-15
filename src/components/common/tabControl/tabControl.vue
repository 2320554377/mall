<!-- 该组件暂没有为每个元素添加路由，看后续老师如何安排 -->
<template>
  <div>
    <ul class="tabControl">
        <!-- 因为使用时只是文字上的不同，所以这里就不用插槽，而是传入数组，根据数组元素来遍历出内容 -->
        <li v-for="(item, index) in tabTitle" 
            :key="item" 
            class="tabControlItem" 
            :style="{'--currentColor':colorStyle}"
            @click="itemClick(index)"
        >
            <!-- <a href=""> -->
                <span :class="{'tabControlcurrent':index === currentIndex}">{{item}}</span>
            <!-- </a> -->
        </li>
    </ul>
  </div>
</template>

<script>
export default {
    name: 'tabControl',
    data(){
        return {
            currentIndex: 0
        }
    },
    props: {
        tabTitle: {
            type: Array,
            default(){
                return []
            },
        },
        colorStyle:{
            type: String,
            default:'#ff8198'
        }
    },
    methods: {
        itemClick(index){
            this.currentIndex = index;
        },
        
    }
}
</script>

<style scoped>
.tabControl{
    display: flex;
    background-color: #fff;
    height: 44px;
    line-height: 44px;
}
.tabControlItem{
    flex: 1;
    text-align: center;
}
.tabControlcurrent{
    color: var(--currentColor);
    padding-bottom: 2px;
    padding: 0 5px 3px;
    border-bottom: 3px var(--currentColor) solid;
}
</style>