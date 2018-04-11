<style lang="less">
    @import "./home.less";
    @import "../../styles/common.less";
</style>
<template>
    <div class="home-main">
       这里是首页，要干嘛干嘛
    </div>
</template>

<script>


export default {
    name: 'home',
    components: {

    },
    data () {
        return {
            
        };
    },
    computed: {
        avatorPath () {
            return localStorage.avatorImgPath;
        }
    },
    methods: {
        
    }
};
</script>
