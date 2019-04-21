<template>
    <div class="type-detail">
      <div class="items-wrap" v-show="item.type" v-for="(item, typeIndex) in store" :key='typeIndex'>
          <div class="items">
            <div class="title">【{{item.type}}】规格项</div>
            <div class="content-wrap">
                <div class="content-items" v-for="(lists, listIndex) in item.list" :key="listIndex">
                    <div class="name">{{item.type}}-{{listIndex}}</div>
                    <div class="data">{{lists}}</div>
                    <div class="del" @click='myDel(typeIndex,listIndex)'>移除</div>
                </div>
            </div>
            <div class="add-content">
                <input type="text" class="add-input" ref='listInput' :data-index="typeIndex">
                <div class="commit" @click="myAdd(typeIndex)">
                添加{{item.type}}规格选项
                </div>
            </div>
          </div>
      </div>
    </div>
</template>

<script>
export default {
    name:'typeDetail',
    props:{
        store:{
            default:[],
            type:Array
        }
    },

    methods:{
        myDel(typeIndex,listIndex){                //通过typeIndex删除对应type的对应listIndex子选项
            this.$emit("dataHandle",'delete', typeIndex , 'list' , listIndex)
        },
        myAdd(typeIndex){                          //点击添加数据渲染dom.并且不为空
            var dom = this.$refs.listInput[typeIndex]
            if(!dom.value){
                alert('内容不可以为空')
                return
            }
            this.$emit("dataHandle",'add' ,typeIndex , 'list' , '', dom.value)
            dom.value = ''
        },
    }
}
</script>

<style lang="stylus" scoped>
.type-detail
    margin-top 10px
    padding 10px 0
    min-width 980px
    display flex
    flex-wrap wrap
    .items-wrap
        box-sizing border-box
        padding 10px
        width 33.33%
        .items
            border 1px solid #7CD13A
            border-radius 10px
            padding 10px
            .title
                padding-bottom 5px
                border-bottom 1px solid #aaa
                color #7CD13A
            .content-wrap
                width 100%
                // background #eee   
                .content-items
                    width 100%
                    display flex
                    margin 10px 0
                    .name
                    .del
                        color #888
                        padding 5px 10px
                        border-radius 5px
                        margin 0 10px
                        height 30px
                        box-sizing border-box
                        cursor pointer
                    .del
                        border 1px solid #7CD13A
                        color #7CD13A
                    .data 
                        flex 1
                        height 30px
                        color #666
                        border 1px solid #888
                        box-sizing border-box
                        border-radius 5px
                        padding 0 5px
                        line-height 30px
            .add-content
                margin-top 10px
                display inline-block
                padding 5px 10px
                border-radius 5px
                background #7CD13A
                color white
                margin-left 10px
                cursor pointer
                .add-input
                    width 100px
                    border-radius 5px
                    height 25px
                    border none
                    outline none 
                    padding 0 5px
                .commit
                    display inline-block
                    margin-left 10px
                    height 25px
                    line-height 25px
</style>
