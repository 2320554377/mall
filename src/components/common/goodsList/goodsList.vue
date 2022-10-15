<template>
  <div class="goodsList">
    <goods-list-item v-for="item in goodsList" :key="item.title">
        <template #goodsImg>
            <img :src="item.show.img" alt="">
        </template>
        <template #goodsInfo>
            <p>{{item.title}}</p>
            <span class="price"><b>￥{{item.price}}</b></span>
            <span class="orgPrice"><s>{{item.orgPrice}}</s></span>
            <p class="sale">已售{{item.sale}}</p>
        </template>
    </goods-list-item>
  </div>
</template>

<script>
import goodsListItem from './goodsListItem.vue'
export default {
    name: 'goodsList',
    props: {
        goodsList: []
    },
    components: {
        goodsListItem
    }
}
</script>

<style>
.goodsList{
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
}
.goods{
    width: 46vw;
    padding-bottom: 10px;
}
.goodsImg img{
    width: 46vw;
    border-radius: 5px;
}
.goodsInfo p{
    /* 超出显示点点点 */
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    padding: 5px 0;
}
.price{
    color: var(--color-tint);
}
.sale, .orgPrice{
    font-size: 15px;
}
</style>