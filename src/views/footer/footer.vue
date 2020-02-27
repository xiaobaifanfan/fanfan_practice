<template>
<div id="footer">
    <div class="section_footer">
    <ul>
        <li class="bottomli" >
            <div class="logo logo1" >安全保障</div>
            <div class="describe" >
                <span>1.资金安全</span>
                <span>2.产品安全</span>
                <br>
                <span>3.交易安全</span>
            </div>
        </li>
        <li class="bottomli">
            <div class="logo logo2" >真实可信</div>
            <div class ="describe" >
                <span>1.第三方监管</span>
                <span>2.认证企业</span>
                <span>3.交易透明</span>
                <span>4.质检机构护航</span>
            </div>
        </li>
        <li class="bottomli"  >
            <div class="logo logo3" >交易方便</div>
            <div class="describe" >
                <span>1.权威信息指导</span>
                <br>
                <span>2.人脉聚集</span>
                <span>3.品类聚集</span>
            </div>
        </li>
        <li class="bottomli"  >
            <div class="logo logo4" >资金支持</div>
            <div class="describe" >
                <span>1.在线融资</span>
                <span>2.为中小企业融资带来了实质性的突破</span>
            </div>
        </li>
        <li class="bottomli" >
            <div class="logo logo5"  >增值服务</div>
            <div class="describe" >
                <span>1.农业咨询</span>
                <span>2.信息技术</span>
                <br>
                <span>3.专业团队的管理服务</span>
    
            </div>

        </li>
    </ul>
</div>
<div id="footer_bottom">
    <div id="footer-link">
        <a href="">企业简介</a>
        <img src="./images/border.jpg">
        <a href="">发展历程</a>
        <img src="./images/border.jpg">
        <a href="">领导关怀</a>
        <img src="./images/border.jpg">
        <a href="">企业荣誉</a>
        <img src="./images/border.jpg">
        <a href="">投资者团队</a>
        <img src="./images/border.jpg">
        <a href="">常见问题</a>
        <img src="./images/border.jpg">
        <a href="">联系方式</a>
        <img src="./images/border.jpg">
        <a href="">服务协议</a>
        <img src="./images/border.jpg">
        <a href="">隐私版权</a>
        <img src="./images/border.jpg">
        <a href="">诚聘精英</a>
        <img src="./images/border.jpg">
        <a href="">媒体报道</a>
    </div>  
    <div id="footer_copyright">
        主办单位：红红火火恍恍惚惚互联网有限公司（可追溯农产品电商交易平台）
    </div>
    <div id="footer_copyright">
        电话：010-7061165  邮箱：honghuohuanghu@163.com 
    </div>
    <div id="footer_copyright">
        Copyright @ 红红火火恍恍惚惚集购网<a href="">www.xxxx.com.cn</a>All rights reserved 版权所有
    </div>

</div>

</div>
</template>
<script>

</script>
<style scoped  lang='scss'>

.section_footer{
    width: 100%;
    height: 80px;
    background: #fafafa;
    position: relative;
}
ul{
    width: 1200px;
    height: 80px;
    position: absolute;
    margin-left: 80px;
    margin-top: 0px;
    background: #fff;
    border:1px solid #dddddd;
}
ul li{
    list-style:none;
    font-size: 16px;
    color:#666;
    cursor: pointer;
    margin-top: 20px;
}
li{
    display: list-item;
    float: left;
    box-sizing:border-box;
    width: 240px;
    height: 40px;
    font-size: 16px;
    color: #666;
    border-right: 2px solid #e5e5e5;

}
li:last-child{
    border-right: none;
}

.logo{
padding: 8px 0 6px;
text-indent: 100px;
}

.logo1{
    background:url(images/footer_01.png) no-repeat 63px center;           
}
.logo2{
    background:url(images/footer_02.png) no-repeat 63px center;           
}
.logo3{
    background:url(images/footer_03.png) no-repeat 63px center;           
}
.logo4{
    background:url(images/footer_04.png) no-repeat 63px center;           
}
.logo5{
    background:url(images/footer_05.png) no-repeat 63px center;           
}
.bottomli:hover .logo{
display: none;
}
.bottomli:hover .describe{
    display: block;
}
.describe{
    display: none;
    text-align: left;
    color: #61a842;
    font-size: 14px;
    padding-left: 24px;
    padding-right: 10px;
}
#footer_bottom{
    position: relative;
    width: 100%;
    text-align: center;
     background: #fafafa;
}
#footer-link{
    font-size: 12px;
}
#footer_copyright{
    color: #707070;
    font-size: 12px;
    margin-top: 10px;
}

</style>
