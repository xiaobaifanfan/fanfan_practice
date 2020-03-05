<template>
    <div class="current-loc">
        <div class="breadcrumbs cle z-detail-box" >
          <div class="menus">
            <a href="">{{proFirstCategory}}</a>
            <code>&gt;</code>
            <a href="">{{proSecondCategory}}</a>
       <!--   <code>&gt;</code>
            {{proThirdCategory}}-->
           
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
            itemGood:'',
            productId:'',
            proTitle:'',
            proFirstCategory:'',
            proSecondCategory:'',
   //         proThirdCategory:''
            
        };
    },
    components: {
        
    },
    props: {
        
    },
    created () {
        var categoryType=0;
        var category_id='';
        var num=0;
       this.productId=this.$route.params.productId;
       //let categoryType='0';
       getGoodsDetail(this.productId)
            .then((response)=> {
                this.itemGood=response.data;
                console.log(this.itemGood);
                this.proTitle=this.itemGood.name;
                this.proSecondCategory=this.itemGood.category.name;//目前商品的目录都是二级目录
                category_id=this.itemGood.category.parent_category;//获取父级种类id(一级)
        
            getCategory({id:category_id}).then((res)=>{
            console.log(res);
            this.proFirstCategory=res.data.name;
            category_id=res.data.parent_category;
            })
            
            }).catch((error)=>{
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
