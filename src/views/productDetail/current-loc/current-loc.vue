<template>
    <div class="current-loc">
        <div class="breadcrumbs cle z-detail-box" >
          <div class="menus">
            <a href="">{{proFirstCategory}}</a>
            <code>&gt;</code>
            <a href="">{{proSecondCategory}}</a>
            <code>&gt;</code>
            {{proThirdCategory}}
            <code>&gt;</code>
            {{proTitle}}
          </div>
      </div>

    </div>
  
</template>
<script> 
import { mapGetters } from 'vuex';
import { getGoodsDetail,getCategory,queryCategorygoods} from '../../../api/api';

export default {
    data () {
        return {
            category_id:'',
            itemGood:'',
            productId:'',
            proTitle:'',
            proFirstCategory:'',
            proSecondCategory:'',
            proThirdCategory:''
            
        };
    },
    components: {
        
    },
    props: {
        
    },
    created () {

       this.productId=this.$route.params.productId;
       getGoodsDetail(this.productId)
            .then((response)=> {
                this.itemGood=response.data;
                console.log(this.itemGood);
                this.proTitle=this.itemGood.name;
                this.proThirdCategory=this.itemGood.category.name;
                this.category_id=this.itemGood.category.id; 
                }).catch(function (error) {
                console.log(error);
            });
        //打印所有一级目录
         getCategory({id:3}).then((response)=>{
         console.log(response);
         console.log("打印所有一级目录")
         }).catch(error=>{
                console.log(error);
         });
        
         
        
        
    },
    watch: {
        '$route'(to,from){
                    //发送Ajax请求
                    this.mes=to.params.id;
                }
    },
    computed: {

    },
    methods: {
        
    }
}
</script>
<style  lang='scss'>
.cle:after{
    visibility:hidden;
    display:block;
    font-size:0;
    content:'\20';
    clear:both;
    height:0
}
.cle{
    *zoom:1
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
    color:#09c762
}
a:focus,area:focus {
    outline:0
}

canvas {
    -ms-touch-action:double-tap-zoom
}

.breadcrumbs {
    padding:0 5px 0 0;
    line-height:38px;
    color:#666
}
.breadcrumbs .menus {
    float:left
}
.breadcrumbs .menus a {
    margin-right:6px
}
.breadcrumbs .right {
    float:right;
    color:#bbb
}
.breadcrumbs .right i {
    font-size:20px;
    margin-right:5px;
    vertical-align:-2px
}
.breadcrumbs .right .code {
    color:#fafafa;
    margin-right:30px;
    display:inline-block
}

</style>
