<template>
    <div id="wrapper">
        <current-loc :curLoc="curLoc"></current-loc>
        <div class="main cle">
            <list-nav :currentCategoryName="currentCategoryName" :cateMenu="cateMenu" :proNum="proNum" :isObject="isObject" @on-change="changeMenu"></list-nav>
            <div class="maincon">
                <price-range :priceRange="priceRange" @on-change="changePrice"></price-range>
                <list-sort @on-sort="changeSort" :proNum="proNum"></list-sort>
                <div class="list-detail">
                    <product-list  :listData="listData"></product-list>
                    <Page pre-text="上一页" next-text="下一页" end-show="false" :page="curPage" :total-page='totalPage' @pagefn="pagefn"></Page>
                </div>
            </div>
        </div>
    </div>

</template>
<script>
    // 产品列表
    import productList from './product-list/productList';
    // 左侧列表导航
    import listNav from './list-nav/listNav';
    // 列表排序
    import listSort from './list-sort/listSort';
    // 翻页
    import page from './page/page';
    // 当前位置(这个有点问题)
    import currentLoc from './current-loc/current-loc';
    // 价格范围
    import priceRange from './price-range/priceRange';

    import { getCategory, getGoods,getGoodsCategory } from '../../api/api'
    export default {
        data () {
            return {
                curPage: 1, // 页码
                top_category: '', // 商品种类
                listData: [],
                cateMenu: {}, //菜单列表
                isObject:true,
                ordering: '-add_time',
                proNum: 0, //商品数量
                curLoc: [{id:'0',name:'首页'},], //当前位置
                priceRange: [], //价格区间
                pricemin: '', //价格最低
                pricemax: '', //价格最高
                pageType:'list',
                searchWord:'',
                currentCategoryName:'',
                currentCategoryType:''
            };
        },
        components: {
            'product-list': productList,
            'list-nav': listNav,
            'list-sort': listSort,
            'Page': page,
            'current-loc': currentLoc,
            'price-range': priceRange

        },
        props: {

        },
        created () {
            this.getAllData ();
        },
        watch: {
            "$route": "getAllData"
        },
        computed: {
            totalPage(){
                return  Math.ceil(this.proNum/12)
            }
        },
        methods: {
            getAllData () {
                console.log(this.$route.params)
                if(this.$route.params.id){
                    this.top_category = this.$route.params.id;
                    this.getMenu(this.top_category); // 获取左侧菜单列表
                }else{
                    this.getMenu(null); // 获取左侧菜单列表
                    this.pageType = 'search'
                    this.searchWord = this.$route.params.keyword;
                }

                this.getListData(); //获取产品列表
                this.getCurLoc(); // 获取当前位置
                this.getPriceRange(); // 获取价格区间
            },
            getListData() {
                if(this.pageType=='search'){
                  getGoods({
                    search: this.searchWord, //搜索关键词
                  }).then((response)=> {
                    this.listData = response.data.results;
                    this.proNum = response.data.count;
                  }).catch(function (error) {
                    console.log(error);
                  });
                }else {
                  getGoods({
                    page: this.curPage, //当前页码
                    top_category: this.top_category, //商品类型
                    ordering: this.ordering, //排序类型
                    pricemin: this.pricemin, //价格最低 默认为‘’ 即为不选价格区间
                    pricemax: this.pricemax // 价格最高 默认为‘’
                  }).then((response)=> {

                    this.listData = response.data.results;
                    this.proNum = response.data.count;
                  }).catch(function (error) {
                    console.log(error);
                  });
                }

            },
            getMenu(id) {
                if(id != null){
                  getCategory({
                    id:this.$route.params.id
                  }).then((response)=> {
                    this.cateMenu = response.data.sub_cat;
                    this.currentCategoryName = response.data.name;
                  }).catch(function (error) {
                    console.log(error);
                  });
                }else {
                  getCategory({}).then((response)=> {
                    this.cateMenu = response.data;
                    this.isObject = false
                  }).catch(function (error) {
                    console.log(error);
                  });
                }

            },

            getCurLoc () { // 当前位置
               getCategory({
                    id:this.top_category
                  }).then((rs)=>{
                  this.currentCategoryType=rs.data.category_type;
                  //console.log(rs.data)
                  //console.log(rs.data.category_type)
                  if(this.currentCategoryType===1){
                    this.curLoc=[{'id':'0','name':"首页"}];
                    this.curLoc.push({id:rs.data.id,name:rs.data.name});
                  }
                  if(this.currentCategoryType===2){
                    this.curLoc=[{'id':'0','name':"首页"}];
                    getCategory({id:rs.data.parent_category}).then((res)=>{
                        this.curLoc.push({name:res.data.name,id:res.data.id})
                        //console.log(res)
                        this.curLoc.push({name:rs.data.name,id:rs.data.id})
                        }).catch((err)=>{
                        console.log(err);
                        })
                  }
                 
                   if(this.currentCategoryType===3)
                  {
                       this.curLoc=[{'id':'0','name':"首页"}];
                       getCategory({'id':rs.data.parent_category}).then((res)=>{
                            getCategory({'id':res.data.parent_category}).then((resdata)=>{
                            this.curLoc.push({name:resdata.data.name,id:resdata.data.id});
                            this.curLoc.push({name:res.data.name,id:res.data.id});
                            this.curLoc.push({name:rs.data.name,id:rs.data.id})
                            })

                       })                  
                 }
                  })
                console.log("当前点击的是category_type:"+this.top_category);
            },
            getPriceRange () {
                this.$http.post('/priceRange', {
                    params: {
                        proType: this.type, //商品类型
                    }
                }).then((response)=> {

                    this.priceRange = response.data;
                }).catch(function (error) {
                    console.log(error);
                });
            },
            changeSort (type) {

                this.ordering = type;
                this.getListData();

            },
            changePrice (data) {
                this.pricemin = data.min;
                this.pricemax = data.max;
                this.getListData();
            },
            changeMenu (id) {
                this.top_category = id; //重新获取
                this.getCurLoc();
                console.log(this.curLoc);
                console.log("--------------------改变目录")
                this.getMenu(id);
                this.getListData();
            },
            pagefn(value){//点击分页
                this.curPage = value.page;
                this.getListData()
            }
        }
}
</script>
<style  lang='scss'>
.maincon {
    width: 970px;
    float: right;
}
</style>
