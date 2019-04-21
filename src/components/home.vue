<template>
    <div class="home">
        <div class="add-project" @click="addProject">+添加规格项</div>
        <add-type @dataHandle="dataHandle" :types="store"></add-type>
        <type-detail  @dataHandle="dataHandle" :store='store'></type-detail>
        <match @upDate="upDate" :matchData="matchData"></match>
    </div>
</template>

<script>
import addType from './addType'
import typeDetail from './typeDetail'
import match from './match'

export default {
    name:'Home',
    components:{
        addType,
        typeDetail,
        match
    },
    watch:{
        store:{
            handler(){
                this.upDate()
            },
            deep:true
        }
    },
    mounted(){
        setTimeout(() => {
            if(confirm('邀您访问我写的移动端音乐APP项目，请问前辈是否愿意浏览一下呢')){
                alert('马上带您跳转，记得切换成mobile模式哦!')
                window.open('http://120.78.124.92')
            }else{
                alert('不看那好吧，打扰了!')
            }
        },5000)
    },
    data(){
        return {
            store:[
                {
                    type:'颜色',
                    list:['牛仔蓝','芭比粉']
                },
                {
                    type:'尺码',
                    list:['m','l','xl','来面试']
                },
            ],
            matchData:[]
        }
    },
    methods:{
        addProject(){
            this.store.push({
                type : "",
                list:[]
            })
        },
        dataHandle(type ,dataIndex , name , listIndex, val){  //增删  数据index type还是list  listIndex val
            let handleType = {          //对数据的处理类型
                'delete':deleteData,
                'add':addData,
            }
            var self = this

            handleType[type]()
            function deleteData(){   //删除数据
                name == 'type' ? self.store.splice(dataIndex,1) : ''
                name == 'list' ? self.store[dataIndex].list.splice(listIndex,1) : ''
            }
            function addData(){     //增加数据
                var myData = self.store
                if(name == 'list'){
                    var flag = myData[dataIndex][name].findIndex((item) => {
                        return val === item
                    })
                    flag === -1 ? self.store[dataIndex].list.push(val) : alert('当前规格已存在，请重新输入')
                }else if(name == 'type'){
                    var flag = myData.findIndex((item) => {
                        return val === item.type
                    })
                    if(flag === -1 ){
                        self.store[dataIndex].type = val
                    }else{
                        alert('当前类型已存在,请重新输入')
                    }
                }
            }
        },
          
        upDate(){                               //对数据进行拼接
            var myStore = this.store
            var len = myStore.length
            if(len == 1){
                this.matchData = myStore[0].list
            }else if(len == 2){
                this.matchData = this.handleArrs(myStore[0].list,myStore[1].list)
            }else if(len > 2){
                this.matchData = this.handleArrs(myStore[0].list,myStore[1].list)
                for(let i=2 ; i < len; i++){    //嵌套处理多个类型的数据
                    this.matchData = this.handleArrs(this.matchData,myStore[i].list)
                }
            }
        },
        handleArrs(oldArr,nowArr){      //每次处理两个数组，在两个的基础上累加。比递归效率更高
            if(!nowArr.length){
                return oldArr
            }
            var newArr = []
            for(let i = 0; i < oldArr.length; i++){
                for(let j = 0 ;j < nowArr.length; j++){
                    newArr.push(oldArr[i] + '_' + nowArr[j])
                }
            }
            return newArr
        },


        // a(...args) {
        //     if(args.length<2){
        //     return args[0]
        //     }
        //     var a=args.shift()
        //     var b=args.shift()
        //     var temp=[]
        //     for (let i = 0,alen; i < alen; i++) {
        //         for (let j = 0,blen; j < blen; j++) {
        //             temp.push(a[i]+b[j])
        //         }
        //     }
        //     args.unshift(temp)
        //     return this.a(...args)
        //     }
           

    }
}
</script>

<style lang='stylus' scoped>
.home 
    width 100%
    position relative
    overflow hidden
    .add-project
        margin 10px 50px
        border-radius 50px
        text-align center
        line-height 40px
        color white
        height 40px
        background #7CD13A
        cursor pointer
</style>
