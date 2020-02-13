
<template>
    <div class="type-scearch">
        <div class="top_search">
            <div>
                <img src="./img/backIcon.png" alt="" class="backIcon" >
            </div>
            <div class="search_c">
                <img src="http://wmall.wochu.cn/h5/classify/img/search-icon.png" alt="">
                <input type="text" id="search_keyc"  @blur="handleTypeVal" />
            </div>
            <div  class="searchIcon">
                <router-link tag="span" to="/searchResult">搜索</router-link>
            </div>
        </div>

        <div class="wrapper">
            <div class="hot-search">
                <p>热门搜索</p>
                <ul class="search_navul">
                    <p v-for="(item,index) in searchList" :key="index">
                            {{item.name}}
                    </p>
                </ul>

            <div class="history-search">
                <p>搜索记录</p>
                <ul>
                    <li v-for="(item,index) in typeVal" :key="index">{{item}}</li>
                </ul>
                <div class="clear_his">清空搜索记录</div>
            </div>

            </div>
        </div>   
           
        </div>
        
   
</template>

<script>
import axios from "axios"

import { async } from 'q';
import {mapState,mapActions} from "vuex"
import ListLi from "../fullGoods/list.vue"

export default {
    name:"typeSearch",
   
    data(){
        return{
            searchList:[],
            typeVal:[],
            typeList:'',
            text:"",
           
        }
    },
    watch:{
        typeVal(newVal,oldVal){
            // console.log(newVal);
            this.text=newVal;
            console.log(this.fullList);
        }
    },
    
    computed:{
        ...mapState({
            fullList:state=>state.typeSearch.fullList,
        })
    },
    created(){
        this.getsearchList();
        this.handleGetTypeSearch();
        // console.log(this.fullList);
    },
    methods:{
        getsearchList(){
                axios.get("http://api9.wochu.cn/client/v1/goods/SearchByTag").then(data => {
                this.searchList=data.data.data;
                console.log(this.searchList)
            });
        },
        handleTypeVal(e){
            var obj={};
            obj.a=e.target.value;
            console.log(obj)
            this.typeVal.push(obj.a);
        },
        ...mapActions({
            handleGetTypeSearch:"typeSearch/handleGetTypeSearch",//从store那action定义过来的
        })
        },
        

}

</script>

<style scoped>
    .top_search{width: 7.5rem;height: 0.88rem;background-color: #fff;position: fixed;top:0;display: flex;justify-content: space-around;align-items: center;padding: 0 0.25rem;z-index: 5;font-size: 0.3rem;}
    .backIcon{width: 0.58rem;}
    .search{width: 0.8rem;}
    .search_c{width: 3.50rem;height: 0.58rem;flex:1;width: 5.5rem;height: .58rem;background-color: #f1f2f6;border-radius: .28rem;margin-right: 0.2rem;}
    .search_c img{float: left;};
    #search_keyc{width: 4.64rem;height: .58rem;float: left;background-color: #f1f2f6;border: 0;}



    .wrapper {position: absolute;top: .88rem;bottom: 0;width: 100%;padding: 0 .2rem; overflow: hidden;background: #fff;}
    .hot-search p{height: 0.4rem;font-size: 0.3rem;color: #333333;margin-top: 0.88rem;margin: 0.2rem 0 0;}
    .search_navul{width: 7.1rem;height: 1.98rem;background-color: #F4F5F7;margin:0 auto;}
    .search_navul p{height:0.58rem;padding:0.04rem 0.2rem;margin:0.2rem;float: left;font-size: 0.26rem;color: #666666;background-color: #fff;}

    .clear_his{text-align: center;margin:0.2rem 0 0.4rem;color: #999;}
    button{background: #fff;border:0;outline:none;}



    .list-li{width: 7.5rem;height: 20rem;background-color: #D8DDE1;margin-top: 1.1rem;}
    .list-li-content{height: 6.08rem;float: left;}
    .list-li-content:nth-of-type(2n+1){padding:0 0.13rem 0.26rem 0.26rem;}
    .list-li-content:nth-of-type(2n){padding:0 0.26rem 0.26rem 0.13rem;}
    .list-li{height: 15rem;overflow: auto;}
    .list-li-content img{width: 3.32rem;height: 3.32rem;}
    .text-content{height: 2.24rem;text-align: center;}
    .list-li-content a{display:block;background-color: #fff;width: 3.36rem;}
    .text-content p{width: 3.29rem;font-size: .3rem;white-space: nowrap;overflow: hidden;}
    .text-content p:nth-of-type(2){color: #c5331e;font-size: .3rem;margin-bottom: 0.2rem;}
    .text-content .add-cart{width: 2.2rem;height: 0.8rem;background-color: #ffe313;border-radius: 0.4rem;margin:0 auto;line-height: 0.8rem;}
</style>
