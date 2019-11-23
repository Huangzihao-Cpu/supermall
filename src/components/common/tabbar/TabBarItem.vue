<template>
<div class="tab-bar-item" @click="btnClick">
   
    <!-- <img src="../../assets/img/TabBar/10.png" alt="">
    <p>首页</p> -->
    <!-- 外层div作用是防止slot被替换覆盖标签上的属性 -->
    <div v-if="!isActive"><slot name="item-icon"></slot></div> 
    <div v-else><slot name="item-icon-active"></slot></div> 
    <div :style="activeStyle"><slot name="item-text"></slot></div> 
    </div>
    
</template> 

<script >

export default ({
    name:"TabBarItem",
    data () {
        return {
        }
    },
    computed: {
        isActive(){
            return this.$route.path.includes(this.path)
        },
        activeStyle(){
            return this.isActive?{color:this.activeColor}:{}
        }
    },
    props: {
        path: String,
        activeColor:{
            type:String,
            default:'red'
        }
    },
    methods: {
        btnClick(){
            // 解决点击多次报错问题
            if(this.$route.path!=this.path){
            // replace 无返回 push有返回
            this.$router.replace(this.path)
            }
        }
    }
})
</script>
<style scoped>
.tab-bar-item {
    flex: 1;
    text-align: center;
    height: 49px;
    font-size: 14px;
}
.tab-bar-item img{height: 24px;width: 24px;vertical-align: middle;margin-top: 4px}
</style>