
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
          <div class="wrapper">
              <swiper :options="swiperOption" ref="mySwiper">
               <swiper-slide v-for='item of swiperList' :key="item.id">
                <img :src="item.imgUrl" class="swiper-img">
                </swiper-slide>
                <div class="swiper-pagination"  slot="pagination"></div>
                <div class="swiper-button-prev" slot="button-prev" @click="goprev"></div>        
                <div class="swiper-button-next" slot="button-next" @click="gonext"></div> 
                </swiper>
          </div>

      </div>
      <div class="right"></div>
    </div>
  </div>
</template>

<script>
 import { swiper, swiperSlide } from 'vue-awesome-swiper';
 import { queryCategorygoods } from '../../api/api';
export default {
  components: {
     swiper,
     swiperSlide,
   },
   data(){
      return {
          list:[],
          swiperOption: {
            pagination: { el: '.swiper-pagination',
             clickable:true
             },
             loop:true,
            autoplay:2500,
            disableOnInteraction:false,
            
           
          },
          swiperList:[{
      id:"0001",
      imgUrl:"http://img1.qunarzz.com/piao/fusion/1801/1a/94428c6dea109402.jpg_640x200_2cf590d8.jpg"
      },{
      id:"0002",
      imgUrl:"http://img1.qunarzz.com/piao/fusion/1802/42/7c92b9a381e46402.jpg_640x200_1cdce2a4.jpg"
      }]
      }
   
},
  created(){
  this.getList();
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
margin-top:5px;
width:100%;
height:auto;
}
.brans .ad_brans_show{
	width:1200px;
	height:195px;
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
  background:#fff;
  margin-top:10px;
  margin-bottom:10px;
}
.new_bg .left{
  border:1px solid red;
  height:500px;
  width:500px;
  box-sizing:border-box;
}

.wrapper >>> .swiper-pagination-bullet-active
    background:#fff;
.wrapper
    overflow: hidden;
    width: 100%;
    height: 0;
    padding-bottom: 30.48%;
    background: #ccc;
    .swiper-img
        width: 100%;

</style>

