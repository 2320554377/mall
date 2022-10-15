<template>
  <div class="tab-bar-item" @click="itemClick">
    <div v-if="!isActive"><slot name="icon"></slot></div>
    <div v-if="isActive"><slot name="active-icon"></slot></div>
    <div :style="isActive?{color: activeColor}:{}"><slot name="text"></slot></div>
  </div>
</template>

<script>
export default {
    name: 'tabBarItem',
    props: {
        path: String,
        activeColor: {
            type: String,
            default: 'pink'
        }
    },
    data(){
        return {
            active: false,
        }
    },
    methods:{
        itemClick(){
            this.$router.replace(this.path);
        },
    },
    computed: {
        isActive(){
            return this.$route.path.indexOf(this.path) !== -1;
        }
    }
}
</script>

<style scoped>
</style>