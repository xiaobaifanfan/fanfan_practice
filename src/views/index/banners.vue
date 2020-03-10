<template>
<div class="banner-warp">
    <div class="banner_left">
        <ul>
          <li v-for="n in 8"></li>
        </ul>
    </div>
     <div class="banner_right">
  右边
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
          <li v-for="n in 5"><img src=""></li>
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
  border:1px solid yellow;
  margin-left:77px;
  box-sizing:border-box;
}
.banner-warp .banner_left ul li{
border-bottom:1px solid #ccc;
height:65px;
box-sizing:border-box;
}
 
.banner-warp .banner_right{
  width:175px;
  height:378px;
  float:right;
  top:30px;
  border:1px solid blue;
  margin-right:77px;
}
.recommandStore{
  border:1px solid red;
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
  border:1px solid #883;
}
.recommandStore ul li img{
  width:100%;
  height:100%;

}
</style>



<script>
  import { swiper, swiperSlide } from 'vue-awesome-swiper'
  import {bannerGoods} from '../../api/api'

  export default {
    components: {
      swiper,
      swiperSlide,
    },
    data() {

      return {
        menu:[],
        swiperOption: {
          pagination: '.swiper-pagination',
          paginationClickable: true,
          autoplay: 2500,
          autoplayDisableOnInteraction: false,
        },
        banners:[]

      }

    },
    methods:{
      getBanner(){
        bannerGoods()
          .then((response)=> {
            console.log(response)
            //跳转到首页页response.body面
            this.banners = response.data
          })
          .catch(function (error) {
            console.log(error);
          });
      },
      getMenu(){
           getCategory().then((response)=> {
                    console.log(response)
                    this.menu = response.data
                })
                .catch(function (error) {
                  console.log(error);
                });
        }
      
    },
    created(){
      this.getBanner(),
      this.getMenu()
    }

  }

</script>
