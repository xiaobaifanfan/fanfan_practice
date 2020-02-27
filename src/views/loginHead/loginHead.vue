<template>
    <div>
    <div id="header">
        <div class="hd_bar" id="userinfo-bar">
        <div class="top_nav">
            <div class="nav_left">欢迎来到<span>农产品电商管理系统</span>~</div>
            <div class="nav_right">
                <div>个人中心|</div>
                <div>商家登陆|</div>
                <div>返回主页|</div>
                <div>退出</div>
            </div>
        </div>
        
            <div class="bd">
                <div class="logo">
                    <a href="#/app/home/index">
                    <img src="../../static/images/loginHead/flow_logo.png"/>
                    </a>
                </div>
                <div class="hd_lbar" style="display: block;" id="ECS_MEMBERZONE">
                    <div><a href="#/app/register/">注册</a></div>
                    <div><a href="#/app/login/">登陆</a></div>
                    <div><a>帮助中心</a></div>
                    <div>咨询热线：<span>12315-10086</span></div>

                </div>
            </div>
        </div>
    </div>
    </div>
</template>

<script>

</script>

<style scoped>
#header {
    width:100%;
     height:150px;
    background: #fff;
}
.hd_bar{
    width:100%;
    height:80px;
}
.top_nav{
    width:100%;
    height:32px;
    position:relative;
    background:#f5f5f5;
    border-bottom:1px solid #e5e5e5;
}
.nav_left{
    float:left;
    font-size:14px;
    position: absolute;
    bottom: 0px;
    left:calc(50% - 1200px / 2);
    padding-bottom:5px;
  }
.nav_left>span{
    font-size:15px;
    font-weight:bold;
}
.nav_right{
    position: absolute;
    bottom: 0px;
    right:calc(50% - 1200px / 2);
    padding-bottom:5px;
}
.nav_right>div{
    float:left;
    font-size: 14px;
     color:#707070; 
}
.logo {
    float:left;
}
.logo>a>img{
    width:350px;
    height: 80px;
    padding-top:30px;
    padding-left:65px;
    float: left;
}

.hd_lbar {
    float:right;
    margin-top:65px;
    margin-right:40px;
    display:none;
}
.hd_lbar>div{
    float:left;
    font-size:16px;
    margin-left:20px;
    color:#707070;
}
.hd_lbar>div:last-child>span{
    color:green;
    font-weight:bold;
}
.hd_lbar a {
    
    color:#707070;
    vertical-align:top
}
.hd_lbar a:hover {
    color:red;
    text-decoration:none;
}

</style>
