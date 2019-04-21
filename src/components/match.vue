<template>
    <div class="match-wrap">
        <div class="button" @click="upDate">
            刷新数据
        </div>
        <div class="content">
            <div class="items" v-for="(item,index) in matchData" :key="index">
                {{item}}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:'Match',
    props:{
        matchData:{
            type:Array,
            default:[]
        }
    },
    methods:{
        upDate(){
            this.$emit('upDate')
        }
    }
}
</script>

<style lang='stylus' scoped>
.button
    display inline-block
    color white
    padding 5px 10px
    background green 
    border-radius 5px
.content
    color black
    .items
        display block
        border-bottom 1px solid #eee
        padding 5px 10px
</style>
