
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
      <div class="right">
        <div class="latest-supply">
              <div class="latest-supply-top">
                  <div class="latest-supply-top-left">
                    <div class="latest-supply-top-title">权威答复</div>
                    <span>服务好人民服务是我们永恒的宗旨</span>
                  </div>
                  <a class="more" href="#">
                    <div class="latest-supply-top-right">更多<span>>></span></div>
                  </a>
              </div>
              <div class="mess-content">
                  <div class="mess-items" v-for="n in 10">
                   <a href="#" class="mess-items-temp" >
                      <div class="lefts">
                          <span>[售后]</span>
                          <div>如何培育出健康有机的西红柿?答：近段时间猪肉价格在很多地区来说还是非常高的，譬如小编家乡这边，猪肉价格还是要三十好几，排骨价格则在四十元以上了，下面惠农网小编就和大家一起来看看近段时间猪肉价格最新行情分析。</div>
                      </div>
                      <span>2020-01-23</span>
                  </a>
                  </div>

               </div>
            </div>

        </div>
            
      </div>
         
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
            this.newgoods=res.data.results.splice(4,4);
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
  position:relative;
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
  margin-left:25px;
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
.new_bg .right{
  //border:1px solid red;
  box-sizing:border-box;
  background:#fff;
  height:520px;
  width:710px;
  position:absolute;
  top:0px;
  margin-left:490px;
}
.mess-content{
  box-sizing:border-box;
  //border:1px solid yellow;
  width:670px;
  margin:0 auto;
  height:460px;
}
.mess-items{
  box-sizing:border-box;
  //border:1px solid red;
  display:flex;
  -webkit-box-align:center;
  align-items:center;
  justify-content:space-between;
  height:40px;
  width:100%;
  margin-bottom:4px;
  background:hsla(0,0%,85%,0.2);
  border-radius:6px;
}
.mess-items-temp{
  align-items:center;
  justify-content:space-between;
  height:40px;
  width:100%;
  margin-bottom:2px;
  position:relative;
}
.mess-items .mess-items-temp:hover{
  background:rgba(0,255,0,0.3);
  font-weight:700;
}
.lefts{
  display:flex;
  font-family:PingFangSC-Regular;
  font-size:16px;
  color:#101010;
  letter-spacing:0px;
}
.mess-content .mess-items .mess-items-temp .lefts span{
  color:#39bf3e;
  padding-left:10px;
  line-height:40px;
  float:left;

}
.lefts div{
  margin-left:10px;
  width:530px;
  line-height:40px;
  white-space:nowrap;
  text-overflow:ellipsis;
  overflow:hidden;
  float:left;
}
.mess-items-temp>span{
  font-family:PingFangSC-Regular;
  font-size:14px;
  color:#909090;
  letter-spacing:0px;
  position:absolute;
  right:5px;
  top:10px;
}
</style>

