
<template>
  <div class="brans">
    <div class="ad_brans_show">
    	<div class="brans_top">
    		<h3 class="J_act_floor">
    			<a herf="#">
    				<img width="1200px" height="80px" src="./images/brans.png">
    			</a>
    		</h3>
    	</div>
    	<div class="brans_bottom">
    		<ul>
    			<li v-for="item in list">
    				<img :src="item.image">
    			</li>
    			

    		</ul>
    	</div>
    </div>
    <div class="new_bg">
      <div class="left">
          <div class="latest-supply">
              <div class="latest-supply-top">
                  <div class="latest-supply-top-left">
                    <div class="latest-supply-top-title">新鲜出炉</div>
                    <span>旨在为您提供最贴心的服务</span>
                  </div>
                  <a class="more" href="#">
                    <div class="latest-supply-top-right">更多<span>>></span></div>
                  </a>
              </div>
              <div class="latest-supply-content">
               <div class="latest-supply-centers">
                <div class="newest-supply" v-for="new_item in newgoods">
                  <router-link :to="'/app/home/productDetail/'+new_item.id">
                      <div class="news-img-div">
                          <img width="200px" height="135px" :src="new_item.goods_front_image">

                      </div>
                      <div class="newest-supply-title">
                        {{new_item.goods_brief}}
                      </div>
                      <div class="newest-supply-price">
                      <span>￥</span>{{new_item.shop_price}}<span>元</span>
                      </div>
                  </router-link>
                </div>       
               </div>
              </div>
          </div>

      </div>
      <div class="right"></div>
    </div>
  </div>
</template>

<script>
 import { swiper, swiperSlide } from 'vue-awesome-swiper';
 import { queryCategorygoods,getGoods } from '../../api/api';
export default {
  components: {
     swiper,
     swiperSlide,
   },
   data(){
      return {
          list:[],
          newgoods:[]
      }
   
},
  created(){
  this.getList();
  this.getNewgoods();
  },
  computed:{
  swiper(){
  return this.$refs.mySwiper.swiper;
  }
  },
  methods:{
  getList(){
              queryCategorygoods()
                .then((res)=> {
                  
                   this.list=res.data[0].brands;
                   this.list=this.list.concat(res.data[1].brands);
                  console.log(this.list);
                })
                .catch(function (error) {
                  console.log(error);
                });
            },
    goprev(){
        this.swiper.slidePrev();
    },
    gonext(){
        this.swiper.slideNext();
    },
    getNewgoods(){
          getGoods({is_new:true}).then((res)=>{
            this.newgoods=res.data.results.splice(0,4);
          })
    }
  }
}
</script>

<style scoped>
div ul li {
	padding:0px;
	margin:0px;
	list-style:none;
}
.brans{
margin-top:10px;
width:100%;
height:auto;
}
.brans .ad_brans_show{
	width:1200px;
	height:180px;
	margin-left:calc(50% - 1200px / 2);
	box-sizing:border-box;
	background:#fff;
}
.brans_bottom{
	margin-top:-5px;
	margin-left:20px;
	margin-right:5px;
	margin-bottom:0px;
}
.brans_bottom ul{
	border-top:1px solid #09c762;
	border-left:1px solid #09c762;
	overflow:hidden;
}
.brans_bottom ul li{
	position:relative;
	width:105px;
	height:80px;
	float:left;
	border-right:1px solid #09c762;
	border-bottom:1px solid #09c762;
}
.brans_bottom ul li img{
	width:100%;
	height:100%;
}
.new_bg{
  width:1200px;
  height:auto;
  margin-left:calc(50% - 1200px / 2);
  background:#dddd;
  margin-top:10px;
  margin-bottom:10px;
}
.new_bg .left{
  border:1px solid #fff;
  background:#fff;
  height:520px;
  width:475px;
  box-sizing:border-box;
}
.latest-supply{
  width:100%;
  height:100%;
}
.latest-supply-top{
  margin-left:20px;
  margin-top:20px;
  align-items:center;
  justify-content:space-between;
  box-sizing:border-box;
  //border:1px solid green;
  position:relative;
}

.latest-supply-top-left{
  display:flex;
}
.latest-supply-top-right{
box-sizing:border-box;
line-height:40px;
font-size:14px;
font-family:MicrosoftYaHei-Bold;
height:100%;
font-weight:bold;
color:#666666;
position:absolute;
top:0px;
right:10px;
}
.latest-supply-top-right:hover{
  color:green;
  font-weight:700;
  font-size:15px;
}
.newest-supply-content{
  height:416px;
  width:100%;
}
.newest-supply-centers{

  -webkit-box-pack:justify;
  justify-content:space-between;
  display:flex;
  flex-wrap:warp;
}
.newest-supply{
  height:200px;
  width:200px;
  margin-top:20px;
  margin-left:23px;
  box-sizing:border-box;
  //border:1px solid yellow;
  float:left;
}
.news-img-div{
  height:135px;
  width:200px;
  overflow:hidden;
}
.new-img-div img{
  height:100%;
  width:100%;
}
.newest-supply a:hover img{
  transform:scale(1.2);
}
.newest-supply-title{
  text-align:center;
  margin-top:6px;
  font-family:PingFangSC-Regular;
  font-size:14px;
  color:#222;
  letter-spacing:0px;
  width:200px;
  white-space:nowrap;
  text-overflow:ellipsis;
  overflow:hidden;
}
.newest-supply:hover .newest-supply-title{
  color:#39bf3e;
}
.newest-supply-price{
  margin-top:0px;
  font-family:PingFangSC-Regular;
  font-size:18px;
  color:#ff442f;
  letter-spacing:0px;
  text-align:center;
}
.newest-supply-price span{
  font-size:12px;
}
.latest-supply-top-title{
  font-family:PingFangSC-Regular;
  font-weight:bold;
  font-size:24px;
  color:#222;
  letter-spacing:0px;
}
.latest-supply-top .latest-supply-top-left span{
  margin-left:10px;
  font-family:MicrosoftYaHei-Bold;
  font-size:12px;
  color:#909090;
  letter-spacing:0px;
  line-height:40px;
}

</style>

