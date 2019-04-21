<template>
    <div class="add-type">
        <div class="types" v-for="(item, index) in types" :key="index">
            <input type="text" class="my-input" :value="item.type" :key='index' ref='myInput'>
            <div class="save" @click="mySave(index)">保存</div>
            <div class="delete" @click="myDel(index)">删除</div>
        </div>
    </div>
</template>

<script>
export default {
    name:'AddType',
    props:{
        types:{
            default:[],
            type:Array
        }
    },
    methods:{
        mySave(index){
            if(!this.$refs.myInput[index].value){
                alert('内容不可以为空')
                return
            }
            this.$emit("dataHandle",'add' ,index , 'type' , '', this.$refs.myInput[index].value)
        },
        myDel(index){
            this.$emit("dataHandle",'delete' ,index , 'type')
        }
    }
}
</script>

<style lang="stylus" scoped>
    .add-type
        width 100%
        display flex
        flex-wrap wrap
        background #eee
        min-width 980px
        .types
            box-sizing border-box
            border 10px solid transparent
            width 33.33%
            height 50px
            display flex
            .my-input
                flex 1
                margin-right 5px
                border-style none
                border-radius 10px
                padding 10px
                outline none 
                border 1px solid #7CD13A           
            .save
            .delete
                cursor pointer
                margin-right 5px
                padding 0 10px
                border-radius 5px
                background #7CD13A 
                color white 
                height 30px 
                line-height 30px 
                font-size 14px
            .delete
                margin 0

</style>
