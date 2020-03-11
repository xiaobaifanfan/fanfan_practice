<template>
<div class="banner-warp">
    <div class="banner_left">
        <ul>
          <li ><div class="box_one"><a href="#/app/home/list/1"><span><i class="iconfont">&#xe602;</i>生鲜食品&nbsp;</span></a></div>
              <div class="box_two" ><a href="#/app/home/list/1">></a></div>
              <div class="box_three"><a href="#/app/home/list/2"><span>精品肉类</span></a>/&nbsp;&nbsp;&nbsp;<a href="#/app/home/list/7"><span>海鲜水产</span></a></div>
          </li>
          <li ><div class="box_one"><a href="#/app/home/list/24"><span><i class="iconfont">&#xe69d;</i>烟酒饮料&nbsp;</span></a></div>
                <div class="box_two" ><a href="#/app/home/list/23">></a></div>
              <div class="box_three"><a href="#/app/home/list/25"><span>白酒</span></a>/&nbsp;&nbsp;&nbsp;<a href="#/app/home/list/29"><span>葡萄酒</span></a></div>
          </li>
          <li ><div class="box_one"><a href="#/app/home/list/40"><span><i class="iconfont">&#xe608;</i>粮食副食&nbsp;</span></a></div>
              <div class="box_two" ><a href="#/app/home/list/39">></a></div>
              <div class="box_three"><a href="#/app/home/list/41"><span>食用油</span></a>/&nbsp;&nbsp;&nbsp;<a href="#/app/home/list/47"><span>米面杂粮</span></a></div>
          </li>
          <li ><div class="box_one"><a href="#/app/home/list/57"><span><i class="iconfont">&#xe603;</i>蔬菜水果&nbsp;</span></a></div>
              <div class="box_two" ><a href="#/app/home/list/56">></a></div>
              <div class="box_three"><a href="#/app/home/list/58"><span>有机蔬菜</span></a>/&nbsp;&nbsp;&nbsp;<a href="#/app/home/list/62"><span>精选蔬菜</span></a></div>
          </li>
          <li ><div class="box_one"><a href="#/app/home/list/74"><span><i class="iconfont">&#xe69c;</i>休闲食品&nbsp;</span></a></div>
              <div class="box_two" ><a href="#/app/home/list/73">></a></div>
              <div class="box_three"><a href="#/app/home/list/75"><span>休闲零食</span></a>/&nbsp;&nbsp;&nbsp;<a href="#/app/home/list/81"><span>糖果</span></a></div>
          </li>
          <li ><div class="box_one"><a href="#/app/home/list/102"><span><i class="iconfont">&#xe60a;</i>奶类食品&nbsp;</span></a></div>
              <div class="box_two" ><a href="#/app/home/list/101">></a></div>
              <div class="box_three"><a href="#/app/home/list/103"><span>进口奶品</span></a>/&nbsp;&nbsp;&nbsp;<a href="#/app/home/list/104"><span>国产奶品</span></a></div>
          </li>
          <li ><div class="box_one"><a href="#/app/home/list/108"><span><i class="iconfont">&#xe6b4;</i>天然干货&nbsp;</span></a></div>
              <div class="box_two" ><a href="#/app/home/list/107">></a></div>
              <div class="box_three"><a href="#/app/home/list/109"><span>菌菇类</span></a>/&nbsp;&nbsp;&nbsp;<a href="#/app/home/list/110"><span>腌干海产</span></a></div>
          </li>
          <li ><div class="box_one"><a href="#/app/home/list/117"><span><i class="iconfont">&#xe607;</i>精选茗茶&nbsp;</span></a></div>
              <div class="box_two" ><a href="#/app/home/list/116">></a></div>
              <div class="box_three"><a href="#/app/home/list/118"><span>白茶</span></a>/&nbsp;&nbsp;&nbsp;<a href="#/app/home/list/119"><span>红茶</span></a></div>
          </li>
        </ul>
    </div>
     <div class="banner_right">
        <button tabindex="-1" class="slider_control slider_control_prev">
          <img height="36px" src="../../static/images/login/slide_l.png">
        </button>
        <ul>
          <li>
            <div class="ad_recommand">
                <div><img src="./images/ad_recomm.jpg"></div>
                <div><img src="./images/ad_recomm.jpg"></div>
                <div><img src="./images/ad_recomm.jpg"></div>
            </div>
          </li>
           <li>
            <div class="ad_recommand">
                <div><img src="./images/ad_recomm2.jpg"></div>
                <div><img src="./images/ad_recomm2.jpg"></div>
                <div><img src="./images/ad_recomm2.jpg"></div>
            </div>
          </li>
        </ul>
        <button tabindex="-1" class="slider_control slider_control_next">
        <img height="36px" src="../../static/images/login/slide_r.png">
        </button>
    </div>
    <div class="banner_swiper">
    <swiper :options="swiperOption">
      <swiper-slide v-for="item in banners" :key="item.goods" >
        <router-link :to="'/app/home/productDetail/'+item.goods" target = _blank > <img :src="item.image" alt="" style="height:380px; width:800px;"/></router-link>
      </swiper-slide>
      <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
    </div>
   
    <div class="recommandStore">
      <ul>
          <li v-for="tempitem in hotgoods"><router-link :to="'/app/home/productDetail/'+tempitem.id"><img :src="tempitem.goods_front_image">
           <s>原价：{{tempitem.market_price}}元</s>
          <strong>惊爆价：</strong><span>￥{{tempitem.shop_price}}元</span></router-link></li>
      </ul>
    </div>
</div>
</template>
<style scoped>
 
  ul li div {
   margin:0;
    padding:0;
  }
  .banner-warp{
    width:100%;
    height:auto;
  }
  .banner_swiper{
    height:380px;
    width:800px;
    margin-left:calc(50% - 800px / 2 + 16px);
    box-sizing:border-box;
    
  }
  .banner-warp .banner_left{
  width:214px;
  height:523px;
  float:left;
  position:relative;
  //border:1px solid yellow;
  margin-left:77px;
  box-sizing:border-box;
  background:#fff;
}
.banner-warp .banner_left ul li{
margin:0px;
padding:0px;
border-bottom:1px solid #ccc;
border-left:1px solid #ccc;
height:65px;
box-sizing:border-box;
position:relative;
}
.box_one{
  padding:0px;
  font-size:17px;
  font-family:PingFangSC-Regular;
  color:#222;
  float:left;
  //font-weight:bold;
}
.iconfont{
  font-size:27px;
}
.box_two{
  float:right;
  margin-top:7px;
  margin-right:35px;
  color:#222;
  font-size:20px;
}
.box_three{
  width:100%;
  position:absolute;
  bottom:3px;
  left:3px;
  font-size:14px;
  color:#646464;
}
a:hover{
  color:#fff;
}
.box_three span{
  margin-right:15px;
  margin-left:5px;
}
.banner-warp .banner_left ul li:hover{
  border-bottom:1px solid #f5f5f5;
  border-right:none;
  background:#30bf3e;
}
.banner-warp .banner_left ul li:hover  div{
  color:#fff;
}
.banner_left ul li:hover a{
  color:#fff;
}
.banner-warp .banner_right{
  width:175px;
  height:378px;
  float:right;
  top:0px;
  border:1px solid blue;
  margin-right:77px;
  box-sizing:border-box;
  position:relative;
}
.banner-warp .banner_right ul li{
  position:absolute;
  width:100%;
  height:100%;

}
.banner-warp .banner_right ul li .ad_recommand{
  box-sizing:border-box;
  border:1px solid red;
}
.banner-warp .banner_right ul li .ad_recommand div:first-child{
  margin-top:0px;
}
.banner-warp .banner_right ul li .ad_recommand div{
  box-sizing:border-box;
  border:1px solid yellow;
  height:122px;
  margin-top:4px;
  width:100%;
}
.banner-warp .banner_right ul li .ad_recommand div img{
  height:100%;
  width:100%;
}
.slider_control{
  position:absolute;
  top:50%;
  width:25px;
  height:35px;
  line-height:35px;
  background-color:#d9d9d9;
  background-color:rgba(0,0,0,0.15);
  margin-top:-20px;
  font-size:20px;
  z-index:2;
  border:none;
  outline:none;
}
.slider_control_prev{
  left:0px;
  border-top-right-radius:18px;
  border-bottom-right-radius:18px;
}
.slider_control_next{
  right:3px;
  border-top-left-radius:18px;
  border-bottom-left-radius:18px;
}
.recommandStore{
  height:133px;
  width:980px;
  margin-left:291px;
  margin-top:10px;
  box-sizing:border-box;
}
.recommandStore ul {
  padding:0;
  margin:0;
}
.recommandStore ul li:first-child{
  margin-left:0px;
}
.recommandStore ul li{
  padding:0;
  margin:0;
  float:left;
  margin-left:7px;
  width:190px;
  height:131px;
  box-sizing:border-box;
  border:1px solid #ccc;
  position:relative;
}
.recommandStore ul li img{
  width:100%;
  height:100%;
}
.recommandStore ul li strong{
  position:absolute;
  bottom:0px;
  right:40px;
  background:rgba(255,255,255,0.7)
}
.recommandStore ul li s{
   position:absolute;
  bottom:0px;
  left:5px;
  background:rgba(255,255,255,0.4)
}
.recommandStore ul li span{
  position:absolute;
  bottom:0px;
  right:0px;
  color:green;
  font-weight:bold;
  background:rgba(255,255,255,0.7)
}
.recommandStore ul li:hover a{
  color:black;
}
.recommandStore ul li:hover{
  border:2px solid green;
}

</style>



<script>

  import { swiper, swiperSlide } from 'vue-awesome-swiper'
  import {bannerGoods,getCategory,getGoods} from '../../api/api'

  export default {
    components: {
      swiper,
      swiperSlide,
    },
    data() {

      return {
        hotgoods:[],
        swiperOption: {
          pagination: '.swiper-pagination',
          paginationClickable: true,
          autoplay: 2500,
          autoplayDisableOnInteraction: false,
        },
        banners:[]

      }

    },
    created(){
      this.getBanner(),
      this.getHotgoods()
    },
    methods:{
      getBanner(){
        bannerGoods()
          .then((response)=> {
            //console.log(response)
            //跳转到首页页response.body面
            this.banners = response.data
          })
          .catch(function (error) {
            console.log(error);
          });
      },
      
      getHotgoods(){
        getGoods({is_hot:false}).then((res)=>{
        this.hotgoods=res.data.results.slice(0,5);
        console.log(this.hotgoods);
        }).catch((err)=>{
        console.log(err)
        })
      }
    }
    

  }

</script>
