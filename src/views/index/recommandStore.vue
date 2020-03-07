<template>
<div class="recommandStore">
<ul>

	<li v-for="n in 5"><img src=""></li>
	
</ul>
</div>

</template>
<style scoped>
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
import {getGoods} from '../../api/api';
export default{
 data(){
 	return{
 	}
 },
 created(){
 
 }
}
</script>