<template>
    <div class="search-panel">
        <el-row class="m-header-searchbar">
            <el-col :span="3" class="left">
                 <img src="//s0.meituan.net/bs/fe-web-meituan/e5eeaef/img/logo.png" alt="美团">
            </el-col>
            <el-col :span="15" class="center">
                <div class="wrapper">
                    <el-input v-model="searchWord" placeholder="请输入内容" @focus="focus" @blur="blur"></el-input>
                    <el-button type="primary" icon="el-icon-search"></el-button>
                    <dl class="hotPlace" v-if="isHotPlace">
                        <dt>热门搜索</dt>
                        <dd v-for="(item,index) in isHotPlaceList" :key="index">
                            <router-link :to="{name: 'goods', params: {name:item}}" >{{item}}</router-link>
                        </dd>
                    </dl>
                    <dl class="searchList" v-if="isSearchList">
                        <dd v-for="(item,index) in searchList" :key="index">
                            <router-link :to="{name: 'goods', params: {name:item}}">{{item}}</router-link>
                        </dd>
                    </dl>
                </div>
                <p class="suggest">
                     <a href="#" v-for="(item,index) in  suggest"  :key="index">{{item}}</a>
                </p>
            </el-col>
        </el-row>
    </div>
</template>

<script>


export default {
    data(){
        return{
            searchWord:'',
            // isHotPlace:false,
            // isSearchList:false,
            isFocus:false,
            hotPlaceList:['京东第一温泉度假村','99旅馆连锁','尚客快捷酒店','7天连锁酒店'],
            searchList:['火锅','火锅自助餐','火锅 重庆'],
            suggest:['京东第一温泉度假村','99旅馆连锁','尚客快捷酒店','7天连锁酒店']
        }
    },
    computed:{
        isHotPlace:function(){
            return this.isFocus && !this.searchWord
        },
        isSearchList:function(){
            return this.isFocus && this.searchWord
        }
    },
    methods:{
        focus(){
            this.isFocus = true
        },
        blur(){
            var self = this;
            setTimeout(function(){
              self.isFocus = false
            },200)
        },


    }
}
</script>

<style lang="scss">
    @import "@/assets/css/public/header/index.scss" ;
    @import "@/assets/css/public/header/search.scss" ;
</style>



