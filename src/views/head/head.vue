<template>
  <div id="header" class="new_header">
    <div class="hd_bar">
        <div class="bd_bar_bd cle">
            <ul class="welcome">
                <li id="ECS_MEMBERZONE" v-if="userInfo.name">
                <router-link :to="'/app/home/member/userinfo'">{{userInfo.name}}</router-link>
                &nbsp;[
                <a @click="loginOut">退出</a>
                ]</li>
                <li id="ECS_MEMBERZONE" v-else>
                <router-link :to="'/app/login'">请登录</router-link>
                <s>|</s>
                 <router-link :to="'/app/register'">免费注册</router-link>
                </li>

            </ul>
            <ul id="userinfo-bar">
                <li class="more-menu" @mouseover="isShowVip=true" @mouseout="isShowVip=false"> <a>会员中心</a><i class="iconfont arrow"> </i>
                    <div class="more-bd" :class="{show:isShowVip}">
                        <div class="list">
                        <router-link :to="'/app/home/member/order'">我的订单</router-link>
                        <router-link :to="'/app/home/member/collection'">我的收藏</router-link>
                        <router-link :to="'/app/home/member/receive'">修改收货地址</router-link>
                        </div>
                    </div>
                </li>
                </ul>
        </div>
    </div>
    <div class="hd_main cle">
        <div class="logo">
        <router-link to="/app/home/index" class="lizi_logo">
            <img src="../../static/images/head/logo.gif" alt="慕学生鲜商城">
        </router-link>

        </div>
        <div class="search_box">
                <input class="sea_input" type="text" name="keywords" id="keyword" v-model="searchWord">
                <button  class="sea_submit" @click="searchSubmit">搜索</button>
        </div>
        <div class="head_search_hot">
         <span>热搜榜：</span>
          <router-link v-for="item in hotSearch" :to="'/app/home/search/'+item.keywords" :key="item.keywords">
            {{item.keywords}}
          </router-link>
        </div>
       
    </div>
    <div class="hd_nav">
        <div class="hd_nav_bd cle">
            <div class="main_nav main_nav_hover" id="main_nav">
                <div class="main_nav_link" @mouseover="overAllmenu" @mouseout="outAllmenu">
                    <a class="meunAll"><img src="../productDetail/images/icon.png"  />全部商品分类
                    </a>
                    <div class="main_cata" id="J_mainCata" v-show="showAllmenu">
                        <ul>
                            <li class="first" v-for="(item,index) in allMenuLabel" @mouseover="overChildrenmenu(index)" @mouseout="outChildrenmenu(index)" @click="closeMenu" v-if="item.is_tab">
                              <h3 style="background:url(../images/1449088788518670880.png) 20px center no-repeat;">
                                <router-link :to="'/app/home/list/'+item.id">{{item.name}}</router-link> </h3>
                                <div class="J_subCata" id="J_subCata" v-show="showChildrenMenu ===index"  style=" left: 215px; top: 0px; border:1px solid orange;">
                                    <div class="J_subView" >
                                      <div v-for="list in item.sub_cat">
                                        <dl>
                                          <h3>
                                            <router-link :to="'/app/home/list/'+list.id">{{list.name}}</router-link>
                                          </h3>
                                          <p>
                                            <router-link  v-for="childrenList in list.sub_cat" :key="childrenList.id" :to="'/app/home/list/'+childrenList.id">&nbsp;&nbsp;&nbsp;&nbsp;{{childrenList.name}}</router-link>
                                          </p>
                                        </dl>
                                        <div class="clear"></div>
                                      </div>
                                    </div>
                                </div>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
            <ul class="sub_nav cle" id="sub_nav">
                <li>
                    <router-link to="/app/home/index">首页</router-link>
                </li>
                <template v-for="(item,index) in allMenuLabel">
                  <li>
                    <div v-if="item.is_tab">
                      <router-link :to="'/app/home/list/'+item.id" >{{item.name}}</router-link>
                    </div>
                  </li>
                </template>

            </ul>
            <div class="hd_cart" id="ECS_CARTINFO"  @mouseover="overShopCar" @mouseout="outShopCar">
             <router-link class="tit" :to="'/app/shoppingcart/cart'" target = _blank>

                    <b class="iconfont">&#xe600;</b>去购物车结算<span><i class="iconfont">&#xe645;</i></span>
                    <em class="num" id="hd_cartnum" style="visibility: visible;">{{goods_list.goods_list.length}}</em></router-link>
                        <div class="list" v-show="showShopCar">
                            <div class="data">
                               <dl v-for="(item,index) in goods_list.goods_list">
                                <dt><router-link :to="'/app/home/productDetail/'+item.goods.id" target = _blank><img :src="item.goods.goods_front_image"></router-link></dt>
                                <dd>
                                  <h4><router-link :to="'/app/home/productDetail/'+item.goods.id" target = _blank>{{item.goods.name}}</router-link></h4>
                                  <p><span class="red">{{item.goods.shop_price}}</span>&nbsp;<i>X</i>&nbsp;{{item.nums}}</p>
                                  <a title="删除" class="iconfont del" @click="deleteGoods(index,item.goods.id)">×</a></dd>
                              </dl>
                            </div>
                            <div class="count">共<span class="red" id="hd_cart_count">{{goods_list.length}}</span>件商品哦~
                                  <p>总价:<span class="red"><em id="hd_cart_total">{{goods_list.totalPrice}}</em></span>
                                  <router-link class="btn" :to="'/app/shoppingcart/cart'" target = _blank>去结算
                                  </router-link>
                                  </p>
                            </div>
                        </div>
            </div>
        </div>
    </div>
    </div>
</template>
<script>
import { mapGetters } from 'vuex';
import cookie from '../../static/js/cookie';
import { getHotSearch, getCategory ,deleteShopCart } from  '../../api/api'
export default {
    data(){
        return {
            hotSearch:[],//热词
            searchWord:'',//搜索词
            showAllmenu:false,//菜单显示控制
            allMenuLabel:[],//菜单
            showChildrenMenu:-1,//菜单显示控制
            showShopCar:false,//购物车显示控制
            isShowVip:false,
        }
    },
    computed: {
        ...mapGetters({
          goods_list: 'goods_list',
          userInfo:'userInfo'
        })
    },
    methods:{
        loginOut(){
            // this.$http.get('/getMenu')
            //     .then((response)=> {

                    //跳转到登录
                    this.$router.push({ name: 'login' })
            //     })
            //     .catch(function (error) {
            //       console.log(error);
            // });
        },
        overAllmenu(){
            this.showAllmenu = true;
        },
        outAllmenu(){
             this.showAllmenu = false;
        },
        closeMenu(){
            this.showAllmenu=false;
        },
        searchSubmit(){
            if(this.searchWord){
                //跳转到登录
                this.$router.push({ name: 'search', params: { keyword: this.searchWord }});
            }
        },
        deleteGoods(index,id) { //移除购物车
            deleteShopCart(id).then((response)=> {
                console.log(response.data);
                this.goods_list.splice(index,1);

                // 更新store数据
                this.$store.dispatch('setShopList');

            }).catch(function (error) {
                console.log(error);
            });
        },
        clickHotWord(word){
            this.searchWord = word;
            //跳转搜索结果页
        },
        overChildrenmenu(index){
            this.showChildrenMenu = index;
        },
        outChildrenmenu(){
            this.showChildrenMenu = -1;
        },
        overShopCar(){
            this.showShopCar = true;
        },
        outShopCar(){
            this.showShopCar = false;
        },
        getMenu(){//获取菜单
          getCategory({
            params:{}
          }).then((response)=> {
                    console.log(response)
                    this.allMenuLabel = response.data
                })
                .catch(function (error) {
                  console.log(error);
                });
        },
        getHotSearch(){//获取热搜
          getHotSearch()
                .then((response)=> {
                    this.hotSearch = response.data
                })
                .catch(function (error) {
                  console.log(error);
                });
        }
    },
    created(){
        this.getMenu()//获取菜单
        this.getHotSearch()//获取热词
        // 更新store数据
        this.$store.dispatch('setShopList');//获取购物车数据
    },

}
</script>
<style scoped  lang='scss'>
html {
    background:#fafafa;
    color:#333;
    _background-attachment:fixed
}
html.isPhone {
    min-width:1196px
}
body,h1,h2,h3,h4,h5,h6,hr,p,blockquote,dl,dt,dd,ul,ol,li,pre,form,fieldset,legend,button,input,select,textarea,th,td {
    margin:0;
    padding:0
}
body,button,input,select,textarea {
    font:12px/1.5 "Microsoft YaHei",Tahoma,Helvetica,Arial,simsun
}
address,cite,dfn,em,var,i {
    font-style:normal
}
ul,ol {
    list-style:none
}
a {
    text-decoration:none;
    color:#333;
    -webkit-transition:color .2s;
    -moz-transition:color .2s;
    -o-transition:color .2s;
    -ms-transition:color .2s;
    transition:color .2s
}
a:hover {
    color:#09c762
}
a:focus,area:focus {
    outline:0
}
fieldset,img {
    border:0
}
#header {
    background:#fff;
    zoom:1
}
#header .hd_main {
    width:1196px;
    margin:15px auto 0;
    position:relative;
    z-index:2001
}

/*需要---------整理*/
.new_header .search_result {
    margin:27px 0 0 -9px;
    width:380px
}
.new_header .hd_cart {
    top:0
}
.new_header .hd_cart .tit {
    border-color:#1e9246
}
.new_header .hd_cart .tit span {
    background-color:#1e9246
}

.hd_cart .tit b {
    color:#aaa;
    margin:0 8px 0 12px;
    font-size:16px;
    cursor:pointer
}
.hd_cart .tit span {
    position:absolute;
    right:0;
    top:-1px;
    display:block;
    width:34px;
    height:28px;
    padding-top:7px;
    background-color:#09c762;
    text-align:center;
    font-size:12px;
    color:#fff;
    cursor:pointer
}
.hd_cart .tit span i {
    display:inline-block;
    width:20px;
    height:20px;
    -webkit-transition:all .3s;
    -moz-transition:all .3s;
    -ms-transition:all .3s;
    transition:all .3s;
    -webkit-backface-visibility:hidden
}
.hd_cart .tit em {
    position:absolute;
    left:17px;
    top:-6px;
    text-align:center;
    font-size:12px;
    color:#fff;
    border:2px solid #fff;
    box-shadow:1px 1px 1px rgba(0,0,0,0.3);
    background-color:#09c762;
    border-radius:10px;
    padding:0 5px;
    line-height:16px;
    visibility:hidden
}
.hd_cart_hover .tit span i {
    -moz-transform:rotate(90deg);
    -webkit-transform:rotate(90deg);
    -ms-transform:rotate(90deg);
    transform:rotate(90deg)
}
#header.new_header .hd_main {
    margin-top:20px;
    height:90px;
    padding-bottom:5px
}

#header.new_header .search_box {
    right:0px;
    top:14px;
    width:460px;
    height:32px;
    border-color:#09c762
}
#header.new_header .search_box .sea_input {
    margin:7px 8px 0;
    width:360px
}
#header.new_header .search_box .sea_submit {
    background-color:#09c762;
    width:80px;
    height:32px
}

/*----------*/
.hd_bar {
    height:34px;
    border-bottom:1px solid #e5e5e5;
    background-color:#f5f5f5;
    position:relative;
    z-index:2002
}


/*hd_bar ul*/

.hd_bar ul {
    padding-top:4px;
    float:left
}
.hd_bar ul.welcome {
    margin-left:-10px
}
.hd_bar ul.welcome li .iconfont {
    color:#999;
    margin-right:4px
}

.hd_bar ul#userinfo-bar {
    float:right
}
.hd_bar ul#userinfo-bar li .vipico {
    width:12px;
    height:17px;
   /*background:url(../../static/images/head/wap.png) no-repeat;*/
    float:left;
    margin-right:4px;
    font-size:18px
}
.hd_bar li {
    float:left;
    position:relative;
    z-index:2000;
    height:17px;
    line-height:17px;
    padding:5px 10px
}
.hd_bar li s {
    color:#ccc;
    margin:0 8px;
    text-decoration:none
}
.hd_bar li a:hover {
    text-decoration:none
}
.hd_bar ul.welcome li .iconfont {
    color:#999;
    margin-right:4px
}
.bd_bar_bd {
    width:1196px;
    margin:0 auto
}
.hd_bar li a.vip-ico {
    background-position:0 3px;
    padding-left:18px
}
.hd_bar li a.svip-ico {
    background-position:0 -23px;
    padding-left:18px
}
.hd_bar li.more-menu {
    padding-right:20px
}
.hd_bar li.more-menu i.arrow {
    position:absolute;
    top:5px;
    right:5px;
    font-size:16px;
    line-height:16px;
    z-index:2002;
    -webkit-transition:all .5s;
    -moz-transition:all .5s;
    -ms-transition:all .5s;
    transition:all .5s;
    color:#bbb;
    -webkit-backface-visibility:hidden
}
.hd_bar li.more-menu .more-bd {
    position:absolute;
    top:37px;
    right:5px;
    z-index:2000;
    opacity:0;
    visibility:hidden;
    box-shadow:1px 1px 3px rgba(100,100,100,0.3);
    -webkit-transition:all .4s;
    -moz-transition:all .4s;
    -ms-transition:all .4s;
    transition:all .4s;
}
.show{
    opacity:1 !important;
    visibility:visible !important;
}

.hd_bar li.hover a.menu-link {
    color:#09c762
}
.hd_bar li.hover i.arrow {
    -moz-transform:rotate(180deg);
    -webkit-transform:rotate(180deg);
    -ms-transform:rotate(180deg);
    transform:rotate(180deg)
}
.hd_bar li.hover .more-bd {
    top:27px;
    opacity:1;
    visibility:visible
}

/*cle*/
.cle:after {
    visibility:hidden;
    display:block;
    font-size:0;
    content:'\20';
    clear:both;
    height:0
}
.cle{
    *zoom:1
}


/*hd-main*/
.logo {
    position:absolute;
    left:10px;
    top:5px;
    z-index:2
}

.search_box {
    position:absolute;
    right:0;
    top:0;
    width:300px;
    height:29px;
    border:2px solid #1e9246;
    border-right:0;
    background-color:#fff;
    overflow:hidden;
    box-shadow:2px 1px 1px rgba(200,200,200,0.5) inset
}
.sea_input {
    float:left;
    width:228px;
    margin:5px;
    height:20px;
    line-height:20px;
    color:#bbb;
    outline:0;
    border:0;
    background:0
}
.sea_submit {
    font-size:15px;
    color:#fff;
    float:right;
    height:29px;
    width:62px;
    padding-left:6px;
    border:0;
    background-color:#1e9246;
    cursor:pointer;
    letter-spacing:5px;
    overflow:hidden
}
.sea_submit:hover {
    color:#ffd736
}


/*热搜榜*/
.head_search_hot {
    position:absolute;
    top:58px;
    right:404px;
    width:450px;
    height:16px;
    overflow:hidden
}
.head_search_hot span {
    color:#999
}
.head_search_hot a {
    margin:0 8px 0 5px;
    color:#666
}
.head_search_hot a.red,.head_search_hot a:hover {
    color:#09c762
}

.hd_nav {
    background-color:#fff;
    height:35px
}

.hd_nav_bd {
    padding-left:214px;
    position:relative;
    z-index:1990;
    width:982px;
    margin:0 auto
}

.main_nav {
    position:absolute;
    top:0;
    left:0;
    z-index:1991
}
.hd_nav .main_nav .main_nav_link {
    width:214px;
    height:35px;
    color:#fff;

    overflow:hidden
}
.hd_nav .main_nav .main_nav_link a.meunAll {
    display:block;
    padding:7px 45px 0 0;
    height:36px;
    font-size:16px;
    text-align:center;
    align-items:center;
    font-weight:bold;
    color:#fff;
    background:#30bf3e;
    font-family:PingFangSC-Regular;
    overflow:hidden;
    border-top-left-radius:5px;
    border-top-right-radius:5px;
}
.hd_nav .main_nav .main_nav_link a.meunAll img{
    width:18px;
    height:15px;
    float:left;
    margin-left:20px;
    margin-top:4px;
}
.hd_nav .main_nav .main_nav_link a:hover {
    text-decoration:none
}
.hd_nav .main_nav .main_nav_link i {
    position:absolute;
    top:10px;
    right:50px;
    -webkit-transition:all .5s;
    -moz-transition:all .5s;
    -ms-transition:all .5s;
    transition:all .5s;
    font-size:12px;
    line-height:16px;
    -webkit-backface-visibility:hidden
}
.hd_nav .main_nav_hover .main_nav_link i {
    -moz-transform:rotate(180deg);
    -webkit-transform:rotate(180deg);
    -ms-transform:rotate(180deg);
    transform:rotate(180deg);
}

.main_cata {
    width:214px;
    height:auto;
    opacity:1;
    position:absolute;
    left:0;
    top:35px;
    z-index:1999;
    padding-bottom:10px;

}
.main_cata ul {
    width:214px;
    overflow:hidden;
    background:rgba(0,80,0,0.9);
    //border-bottom:1px solid #09c726;
}
.main_cata li {
    width:100%;
    height:64.5px;
    border-bottom:1px solid #ccc;
    overflow:hidden;
    font-size:0;
}
.main_cata li a {
    font-size:14px
}
.main_cata li h3 {
    text-indent:58px;
}
.main_cata li h3 a {
    font-size:13px;
    line-height:64.5px;
    font-family:Arial;
    color:#fff;
}
.main_cata li .bd {
    padding:0;
    margin-right:-10px;
    height:43px;
    overflow:hidden
}
.main_cata li .bd a {
    color:#999;
    display:inline-block;
    margin-right:14px;
    line-height:22px
}
.main_cata li.last {
    padding:0;
    box-shadow:0 4px 3px rgba(200,200,200,0.3)
}
.main_cata li.last a {
    display:inline-block;
    width:48%;
    height:54px;
    text-align:center;
    line-height:54px;
    overflow:hidden;
    font-weight:bold;
    font-size:14px
}
.main_cata li.last a.no2 {
    border-left:1px solid #ccc
}
.main_cata li.current {
    background-color:#eee;
    border-right-color:#eee;
    box-shadow:0 0 10px #eee
}
.main_cata li.current h3 a,.main_cata li.current a:hover {
    color:#09c762
}
.J_subCata {
    position:absolute;
    z-index:1998;
    -webkit-transition:all .2s ease;
    -moz-transition:all .2s ease;
    -ms-transition:all .2s ease;
    -o-transition:all .2s ease;
    transition:all .2s ease
}
.J_subCata .J_subView {
    border:1px solid #ccc;
    width:780px;
    height:520px;
    min-height:228px;
    overflow:hidden;
    background:rgba(0,255,0,0.3);
    position:relative;
    box-shadow:3px 3px 4px rgba(0,0,0,0.3);
}
.J_subView>div>dl{
    box-sizing:border-box;
    border:1px solid rgba(255,255,255,0);
    margin:0px;
    padding:0px;
    height:65px;
}
.J_subCata .J_subView dl h3{
    height:36px;
    font-size:16px;
    margin-top:-15px;
    margin-left:-20px;
    width:100%;
}
.J_subCata .J_subView dl h3 a{
      color:black;
      font-size:16px;
      font-weight:bold;
}
.J_subCata .J_subView dl h3 a:hover{
    color:red;
}
.J_subCata .J_subView dl p{
    overflow:hidden;
    padding-top:10px;
    margin-left:30px;
    font-weight:bold;

}
.J_subCata .J_subView dl p a{
    color:#fff;
    font-size:15px;
    margin-right:15px;
    display:inline-block;
    white-space:nowrap;
}
.J_subCata .J_subView dl p a:hover{
    color:red;
}
.clear {
    clear: both;
    height:0;
    font-size:0;
    line-height:0;
    overflow:hidden
}

.hd_nav .sub_nav {
    float:left
}
.hd_nav .sub_nav li {
    float:left;
    height:35px;
    overflow:hidden;
    font-size:14px;
}
.hd_nav .sub_nav li a {
    display:inline-block;
    height:21px;
    overflow:hidden;
    padding:7px 18px;
    color:#646464;
}
.hd_nav .sub_nav li.current a,.hd_nav .sub_nav li a:hover {
    color:#09c762;
    font-weight:700;
    text-decoration:none
}

.hd_cart {
    top:0
}
.hd_cart {
    position:absolute;
    right:0;
    top:30px;
    z-index:200
}
.hd_cart a:hover {
    text-decoration:none
}
.new_header .hd_cart .tit {
    border-color:#1e9246
}
.new_header .hd_cart .tit span {
    background-color:#1e9246
}



.hd_cart .tit {
    display:block;
    width:168px;
    height:28px;
    padding-top:5px;
    position:relative;
    z-index:10;
    background:#f8f8f8;
    border:1px solid #ccc;
    border-right:0;
    font-size:14px;
    color:#666
}
.hd_cart .tit b {
    color:#aaa;
    margin:0 8px 0 12px;
    font-size:16px;
    cursor:pointer
}
.hd_cart .tit span {
    position:absolute;
    right:0;
    top:-1px;
    display:block;
    width:34px;
    height:28px;
    padding-top:7px;
    background-color:#09c762;
    text-align:center;
    font-size:12px;
    color:#fff;
    cursor:pointer
}
.hd_cart .tit span i {
    display:inline-block;
    width:20px;
    height:20px;
    -webkit-transition:all .3s;
    -moz-transition:all .3s;
    -ms-transition:all .3s;
    transition:all .3s;
    -webkit-backface-visibility:hidden
}
.hd_cart .tit em {
    position:absolute;
    left:17px;
    top:-6px;
    text-align:center;
    font-size:12px;
    color:#fff;
    border:2px solid #fff;
    box-shadow:1px 1px 1px rgba(0,0,0,0.3);
    background-color:#09c762;
    border-radius:10px;
    padding:0 5px;
    line-height:16px;
    visibility:hidden
}
.hd_cart_hover .tit span i {
    -moz-transform:rotate(90deg);
    -webkit-transform:rotate(90deg);
    -ms-transform:rotate(90deg);
    transform:rotate(90deg)
}

.hd_bar li.more-menu .more-bd {
    position:absolute;
    top:37px;
    right:5px;
    z-index:2000;
    opacity:0;
    visibility:hidden;
    box-shadow:1px 1px 3px rgba(100,100,100,0.3);
    -webkit-transition:all .4s;
    -moz-transition:all .4s;
    -ms-transition:all .4s;
    transition:all .4s
}
.hd_bar .more-bd .list {
    width:94px;
    border:1px solid #ddd;
    background:#fff
}
.hd_bar .more-bd .hezuo_list {
    width:72px
}
.hd_bar .more-bd .list a {
    display:block;
    background-color:#fff;
    border-bottom:1px dashed #d7d7d7;
    padding:6px 10px;
    height:17px;
    overflow:hidden
}
.hd_bar .more-bd .list a:hover {
    background:#f8f8f8;
    color:#333;
    text-decoration:none
}

.hd_bar li.hover .more-bd {
    top:27px;
    opacity:1;
    visibility:visible
}

.hd_cart .list {
    width:220px;
    position:absolute;
    right:0;
    top:35px;
    border:1px solid #09c762;
    background-color:#fff;
    -webkit-transition:all .3s;
    -moz-transition:all .3s;
    -ms-transition:all .3s;
    transition:all .3s
}
.hd_cart_hover .list {
    visibility:visible;
    opacity:1;
    top:34px
}
.hd_cart .list .load {
    height:100px
}
.hd_cart .list .fail {
    padding:10px 20px 20px;
    text-align:center;
    color:#999
}
.hd_cart .list .fail i {
    font-size:30px;
    color:#ddd
}
.hd_cart .list .data {
    position:relative;
    zoom:1;
    width:220px;
    overflow:hidden
}
.hd_cart .list .data_over {
    max-height:318px;
    _height:318px;
    overflow-y:auto
}
.hd_cart .list dl {
    padding:5px 8px;
    width:204px;
    height:42px;
    overflow:hidden;
    background:#fff;
    border-bottom:1px dashed #ddd
}
.hd_cart .list dt {
    float:left;
    width:42px
}
.hd_cart .list dt img {
    width:40px;
    height:40px;
    vertical-align:top;
    border:1px solid #ccc
}
.hd_cart .list dd {
    float:right;
    width:152px;
    color:#666;
    padding-top:2px;
    position:relative
}
.hd_cart .list .data_over dl {
    width:189px
}
.hd_cart .list .data_over dd {
    width:137px
}
.hd_cart .list dd a {
    color:#666
}
.hd_cart .list dd h4 {
    height:20px;
    overflow:hidden
}
.hd_cart .list dd i {
    display:inline-block;
    font-size:10px;
    -webkit-transform:scale(0.7)
}
.hd_cart .list dd .del {
    position:absolute;
    top:20px;
    right:0;
    color:#bbb
}
.hd_cart .list .count {
    background-color:#f5f5f5;
    color:#666;
    padding:10px 8px 14px;
    position:relative
}
.hd_cart .list .count span {
    margin:0 3px
}
.hd_cart .list .count em {
    font-size:14px;
    margin-left:2px
}
.hd_cart .list .count p {
    margin-top:12px
}
.hd_cart .list .count a {
    position:absolute;
    top:35px;
    right:10px;
    border-radius:0;
    border:0;
    padding:5px 15px 7px;
    font-size:14px;
    background: #09c762;
    color:#fff;
    &:hover{
      background: #1e9246;
    }
}





</style>
