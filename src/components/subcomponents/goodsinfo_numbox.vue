<template>
<!-- 问题：我不知道什么时候能够拿到 max值，但总归有一个时刻，会得到真正的max值 -->
<!-- 我可以使用watch属性监听父组件传递过来的max值 不管watch 会被触发几次，但是最后一次
肯定是一个合法的max数值 -->
    <div class="mui-numbox" data-numbox-min='1'>
        <button class="mui-btn mui-btn-numbox-minus" type="button">-</button>
        <input id="test" class="mui-input-numbox" type="number" value="1" 
        @change="countChange" ref="numbox"/>
        <button class="mui-btn mui-btn-numbox-plus" type="button">+</button>
    </div>


    <!-- 分析：子组件什么时候把 数据传递给父组件 -->
    <!-- 文本框数据被修改的时候 将数据传递给父组件 -->
</template>

<script>
import mui from '../../lib/mui/js/mui.min.js'
export default {
    mounted() {  
    //初始化数字选择框组件
     mui(".mui-numbox").numbox()   
     console.log(this.max)
    },
    methods:{
        countChange(){
            // 每当 文本框数据被修改的时候，立即把 最新的数据 通过事件调用，传递给父组件
            this.$emit("getcount", parseInt(this.$refs.numbox.value))
        }
    },
    props:["max"],
    watch:{
        // 属性监听
        'max': function(newVal,oldVal){
            // 使用你JS API 设置 numbox的最大值
            mui(".mui-numbox").numbox()
            .setOption('max',newVal)
        }
    }
}
</script>

<style lang="scss" scoped>

</style>