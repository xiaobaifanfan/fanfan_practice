<template>
<div id="moreDetail">
<div class="box_one">
	<h3>
		<img src="./images/icon-gt.png"/>
		<span>商品参数</span>
	<img src="./images/icon-lt.png"/>
	</h3>
	<div class="con">
		<table  style="width: 100%">
			<tr>
				<td style="width: 350px">报价时间：{{date}}</td>
				<td style="width: 300px">库存：{{amount}}吨</td>
				<td style="width: 300px">交割地：{{position1}}</td>
			</tr>
			<tr>
				<td style="width: 350px">仓库所在地：{{position2}}</td>
				<td style="width: 300px">包装方式：{{display_way}}</td>
				<td style="width: 300px">执行标准：{{}}</td>
			</tr>
		</table>
	</div>
</div>

<div class="box_one">
	<h3>
		<img src="./images/icon-gt.png"/>
		<span>商品详情</span>
	<img src="./images/icon-lt.png"/>
	</h3>
	<div class="con"></div>
</div>

</div>
</template>
<script>
export default{
	data(){
		return{
			date:'',
			amount:'',
			position1:'',
			position2:'',
			display_way:''
		}
	}
}
</script>
<style scoped>
#moreDetail{
	float: left;
	width: 970px;
	margin-top:15px;
}
.box_one{
	font-size: 14px;
	color: #666;
	border: 1px solid #e5e5e5;
	margin-bottom: 15px;
}
.box_one>h3{
	background: #f2f2f2;
	padding: 14px 16px;
	border-bottom: 1px solid #e5e5e5;
	color: #61a842;
	font-size: 16px;
	margin: 0;
}
.box_one>h3>img{
	vertical-align: middle;
}
.box_one>h3>span{
	margin: 0 5px;
}
.box_one>.con{
	padding: 14px 18px;
	line-height: 1.5;
}
.box_one>.con>table{
	border-spacing: 10px 0px;
}
.box_one>.con>table>tr>td{
	padding: 5px 0;
}
</style>
