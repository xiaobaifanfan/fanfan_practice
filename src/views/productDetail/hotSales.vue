<template>
<div class="z-detail-right">
    <div class="tabs_bar_right">
        <div class="tabs_bar2">
        <s></s>
        <span>热卖商品</span></div>
    </div>
    <div class="hot_box">
        <ul>
            <li v-for="item in show_hotProduct">
              <router-link :to="'/app/home/productDetail/'+item.id">
                <div class="container">
                    <img class="content_img" :src="item.goods_front_image">
                    <p class="hot_price">￥{{item.shop_price}}元</p>
                </div>
                <p class="hot_name">{{item.name}}</p>
              </router-link>
            </li>
        </ul>
        <div style="margin-bottom:-12px;" >
            <i id="pre_hotGoods" style="padding-left:30px;font-weight:bold;color:#999" @click="pre_hotGoods">上一页</i>
            <i id="next_hotGoods" @click="next_hotGoods" style="padding-left:35px;font-weight:bold">下一页</i>
        </div>
    </div>
</div>

</template>
<script>
    import { getGoods } from '../../api/api';

    export default {
        data () {
            return {
                hotProduct: [
                ],
                current_page:1,
                pageNum:0,
                show_hotProduct:[]

            };
        },
        props: {

        },
        created () {
            this.getHotSales();
        },
        watch: {

        },
        computed: {
            
        },
        methods: {
            getHotSales() { //请求热卖商品
              getGoods({
                is_hot:false,
              })
                .then((response)=> {
                    console.log(response.data);
                    this.hotProduct = response.data.results;
                    this.show_hotProduct = response.data.results.slice(0,3);
                    this.pageNum=Math.ceil(this.hotProduct.length/3);
                    console.log(this.hotProduct.length+"d"+this.pageNum);
                }).catch(function (error) {
                    console.log(error);
                });
            },
            next_hotGoods(){
            if(this.current_page===this.pageNum){
            document.getElementById('next_hotGoods').style.color='#999';
            }else{
            this.current_page++;
            document.getElementById('pre_hotGoods').style.color='black';
            document.getElementById('next_hotGoods').style.color='black';
            }
            console.log(this.current_page)
            },

            pre_hotGoods(){
            if(this.current_page===1){
            document.getElementById('pre_hotGoods').style.color='#999';
            }else{
            this.current_page--;
            document.getElementById('pre_hotGoods').style.color='black';
            document.getElementById('pre_hotGoods').style.color='black';
            }
            
            console.log(this.current_page)
            }
        }
    }
</script>
<style scoped>

html {
    background:#fafafa;
    color:#333;
    _background-attachment:fixed
}

body,p,ul,ol,li {
    margin:0;
    padding:0
}
body{
    font:12px/1.5 "Microsoft YaHei",Tahoma,Helvetica,Arial,simsun
}

ul,ol {
    list-style:none
}
img {
    border:0
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
    color:red;
}
a:focus,area:focus {
    outline:0
}
::selection {
    background:#09c762;
    color:#fff
}
canvas {
    -ms-touch-action:double-tap-zoom
}


.z-detail-right {
    width:200px;
    float:right
}
.tabs_bar_right {
    height:25px;
    width:216px;
    position:relative;
}
.tabs_bar2 {
    height:20px;
    padding:0 35px;
    display:block;
    line-height:48px;
    text-align:center;
}
.tabs_bar2>s{
    position:absolute;
    top:20px;
    left:30px;
    width:140px;
    height:0px;
    border-top:1px dotted #c9c9c9;
    text-decoration:none;
}
.tabs_bar2>span{
    position:absolute;
    color:#999;
    text-align:center;
    height:20px;
    line-height:20px;
    top:10px;
    left:35%;
    background-color:#fafafa;
    padding:0;
}

.hot_box {
    padding:10px;
    border:1px solid #ccc;
    border-top:0;
}
.hot_box ul li {
    margin-bottom:10px;
}
li{
    height:174px;
}
.container{
    display:block;
    text-align:center;
    color:#625742;
    zoom:1;
    cursor:pointer;
    position:relative;
}
.content_img{
    vertical-align:middle;
    max-height:140px;
    max-width:140px;
    border:0;
}
p.hot_price {
    position:absolute;
    font-family:Arial;
    color:#09c762;
    font-weight:bold;
    line-height:20px;
    background-color:rgba(255,2255,255,0.7);
    width:140px;
    margin-left:17px;
    bottom:0px;
    text-align:center;
}
p.hot_name{
    text-overflow:ellipsis;
    overflow:hidden;
    white-space:nowrap;
    display:block;
    margin-top:5px;
}


</style>
