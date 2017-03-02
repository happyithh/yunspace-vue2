<script src="../../assets/libs/jquery/jquery-3.1.1.min.js"></script>
<template>
<div class="openshop-box">
    <!--banner板块-开始-->
    <div class="banner-search">
        <h1>我要开店</h1>
        <a class="btnopenshop" href="http://www.yunspace.com.cn/retail">立即提交需求</a>
        <!--搜索-->
        <div class="search">
            <h2>找到适合你的商业短租场地</h2>
            <div class="inputbox clearfix">
                <input class="searchInputVal" v-model="homeSearchCondition.q.keyword_cont" @keyup.enter="goSpaceSearch" type="text" placeholder="商圈／地标／机场／火车站／场地名">
                <button class="searchbtn" @click="goSpaceSearch">搜&nbsp;索</button>
            </div>
            <div class="hot clearfix">
                <p>热点：</p>
                <div class="hotlist">
                    <router-link v-for="item in cityHotKeyword" :to="{ path: '/spaces', query: { q : item }}">
                        {{item}}
                    </router-link>

                </div>
            </div>
        </div>
    </div>
    <!--banner板块-结束-->

    <!--主题部分-开始-->
    <div class="w1200 mt30">
        <div class="optitle clearfix">
            <h3>我要开店</h3>
            <!--<a class="more" href="javascript:;">查看更多<i class="icon icon-arrowright"></i></a>-->
        </div>
        <ul class="openshop clearfix">
            <li class="dob">
                <a @click="spaceSearchFixed('Pop Up Store')" href="javascript:;">Pop Up Store<span><br/>（快闪店/体验店/游击店）</span></a>
            </li>
            <li>
                <a @click="spaceSearchFixed('店中店')" href="javascript:;">店中店</a>
            </li>
            <li>
                <a @click="spaceSearchFixed('市集,展')" href="javascript:;">市集/展</a>
            </li>
            <!--<li class="dob">-->
                <!--<a @click="spaceSearchFixed('售卖机,展示点')" href="javascript:;">DP点<span><br/>（售卖机／展示点）</span></a>-->
            <!--</li>-->
            <!--<li>-->
                <!--<a @click="spaceSearchFixed('集合点')" href="javascript:;">集合点</a>-->
            <!--</li>-->
        </ul>
    </div>

    <!--合作流程-->
    <div class="w1200 mt30">
        <div class="optitle clearfix">
            <h3>合作流程</h3>
            <!--<a class="more" href="javascript:;">查看更多<i class="icon icon-arrowright"></i></a>-->
        </div>
        <ul class="cont opprocess clearfix">
            <li>
                <div class="ibox">
                    <span class="img"></span>
                    <p>提交需求</p>
                </div>
                <span class="iconright"></span>
            </li>
            <li>
                <div class="ibox">
                    <span class="img"></span>
                    <p>匹配场地&场景</p>
                </div>
                <span class="iconright"></span>
            </li>
            <li>
                <div class="ibox">
                    <span class="img"></span>
                    <p>确定合作方式</p>
                </div>
                <span class="iconright"></span>
            </li>
            <li>
                <div class="ibox">
                    <span class="img"></span>
                    <p>品牌／内容落地</p>
                </div>
                <span class="iconright"></span>
            </li>
            <li>
                <div class="ibox">
                    <span class="img"></span>
                    <p>申请加入V+品牌库</p>
                </div>
                <span class="iconright"></span>
            </li>
            <li>
                <div class="ibox">
                    <span class="img"></span>
                    <p>平台战略推广与支持</p>
                </div>
            </li>
        </ul>
    </div><!--合作流程-end-->

    <!--专题-->
    <div class="w1200 mt30">
        <div class="optitle clearfix">
            <h3>专题</h3>
            <router-link class="more" to="/found">查看更多<i class="icon icon-arrowright"></i></router-link>
            <!--<a class="more" href="javascript:;">查看更多<i class="icon icon-arrowright"></i></a>-->
        </div>
        <ul class="cont opsubject clearfix">
            <li v-for="item in specials">
                <a class="img" target="_blank" :href="item.special_url ? item.special_url : '/article/' + item.id"><img :src="item.img_paths.length > 0 ? item.img_paths[0]['url_400_267'] : ''"></a>
                <div class="text">
                    <a class="title" target="_blank" :href="'/article/'+item.id">{{item.title}}</a>
                    <p>{{item.abstract}}</p>
                </div>
            </li>
        </ul>
    </div><!--专题-end-->

    <!--空间分类-->
    <div class="w1200 mt30 clearfix">
        <div class="optitle clearfix">
            <h3>空间分类</h3>

        </div>
        <div class="fl cont classfiylist clearfix">
            <a class="art" @click="spaceSearchTypeFixed(115)">
                <i class="icons"></i>
                <p>艺术画廊</p>
            </a>
            <a class="show" @click="spaceSearchTypeFixed(113)">
                <i class="icons"></i>
                <p>秀场展馆</p>
            </a>
            <a class="business" @click="spaceSearchTypeFixed(114)">
                <i class="icons"></i>
                <p>商业广场</p>
            </a>
            <a class="starbusiness" @click="spaceSearchTypeFixed(120)">
                <i class="icons"></i>
                <p>星级酒店</p>
            </a>
            <a class="movies" @click="spaceSearchTypeFixed(117)">
                <i class="icons"></i>
                <p>影院剧院</p>
            </a>
            <a class="highclubs" @click="spaceSearchTypeFixed(119)">
                <i class="icons"></i>
                <p>高端会所</p>
            </a>
            <a class="conference" @click="spaceSearchTypeFixed(121)">
                <i class="icons"></i>
                <p>会务中心</p>
            </a>
            <a class="stadia" @click="spaceSearchTypeFixed(116)">
                <i class="icons"></i>
                <p>体育场馆</p>
            </a>
        </div>
        <router-link class="fr classfiymore" tag="a" to="/spaces?type=all">
            <i class="icons"></i>
            <p>更多分类</p>
        </router-link>
    </div><!--空间分类-end-->

    <!--TOP榜单-->
    <div class="w1200 mt30">
        <div class="optitle clearfix">
            <h3>TOP榜单</h3>
            <router-link class="more" to="/found?newsType=19&selectType=newsType&selectTypeKey=19">查看更多<i class="icon icon-arrowright"></i></router-link>

        </div>
        <ul class="cont optoplist clearfix">
            <li v-for="topList in topLists">
                <a target="_blank" :href="'/article/'+topList.id">
                    <img :src="topList.img_paths.length > 0 ? topList.img_paths[0]['url_400_267'] : ''">
                    <p>{{topList.title}}</p>
                </a>
            </li>
        </ul>
    </div><!--TOP榜单-end-->

    <!--推荐空间-开始-->
    <div class="w1200 mt30">
        <div class="optitle clearfix">
            <h3>推荐空间</h3>
            <router-link class="more" to="/spaces">查看更多<i class="icon icon-arrowright"></i></router-link>
            <!--<a class="more" href="javascript:;">查看更多<i class="icon icon-arrowright"></i></a>-->
        </div>
        <ul class="cont opvenues-recommend clearfix">
            <li v-for="item in recommendSpace">

                <a :href="'/space/'+item.id" class="img">
                    <img :src="item.img_paths.length > 0 ? item.img_paths[0]['url_400_267'] : ''">
                    <div class="price">{{item.special_price}}</div>
                    <!--<div class="collect-mask">-->
                    <!--<div class="collect icons icon-collectbgmore-hv"></div>-->
                    <!--<div class="mask"></div>-->
                    <!--</div>-->
                </a>




                <div class="text">
                    <a class="title" target="_blank" :href="'/space/'+item.id">{{item.name}}</a>
                    <p>{{item.introduced}}</p>
                    <p>{{item.city_name}}&nbsp;{{item.areas}}<br>{{item.address}}</p>
                </div>
                <div class="icons icondou"></div>
            </li>
        </ul>
    </div><!--推荐空间-结束-->

    <!--精选案例-开始-->
    <div class="w1200">
        <div class="optitle clearfix">
            <h3>精选案例</h3>
            <router-link class="more" to="/found?caseType=6&selectType=caseType&selectTypeKey=6">查看更多<i class="icon icon-arrowright"></i></router-link>
            <!--<a class="more" href="javascript:;">查看更多<i class="icon icon-arrowright"></i></a>-->
        </div>
        <ul class="cont selectedcases clearfix">
            <li v-for="item in selectedCase">
                <div class="textinfo">
                    <a class="title" target="_blank" :href="'/article/'+item.id">{{item.title}}</a>
                    <p>{{item.abstract}}</p>
                </div>
                <a class="btnlook" target="_blank" :href="'/article/'+item.id">查看<i class="icon icon-arrowright"></i></a>
                <a class="img" target="_blank" :href="'/article/'+item.id"><img :src="item.img_paths.length > 0 ? item.img_paths[0]['url_400_400'] : ''"></a>
            </li>
        </ul>
    </div><!--精选案例-结束-->

    <!--合作伙伴-开始-->
    <div class="w1200 mt30">
        <div class="optitle clearfix">
            <h3>合作伙伴</h3>
        </div>
        <div class="cont partners clearfix">
            <div id="Slide1" class="zy-Slide">
                <section class="icon-arrowleft"></section>
                <section class="icon-arrowright"></section>
                <ul>
                    <li><img src="/static/images/openshop/logo/1.png" /></li>
                    <li><img src="/static/images/openshop/logo/2.png" /></li>
                    <li><img src="/static/images/openshop/logo/3.png" /></li>
                    <li><img src="/static/images/openshop/logo/4.png" /></li>
                    <li><img src="/static/images/openshop/logo/5.png" /></li>
                    <li><img src="/static/images/openshop/logo/6.png" /></li>
                    <li><img src="/static/images/openshop/logo/7.png" /></li>

                </ul>
            </div>
            <!--<div class="abouttext">-->
                <!--<p>TASTE is hidden deep in Shanghai’s Tianzifang area</p>-->
                <!--<h5>A Matter of TASTE</h5>-->
            <!--</div>-->
        </div>
    </div><!--合作伙伴-结束-->

</div>
</template>

<script>

    import Lib from 'assets/Lib.js';
    import zyslide from 'assets/libs/jquery/zySlide/jquery.zySlide.js';
    require ('assets/css/component.css');
    require ('assets/css/openshop.css');
    require ('assets/css/jquery.zySlide.css');
    export default {
        data(){
            return {
                specials:[ ],
                topLists:[ ],
                recommendSpace:[ ],
                selectedCase:[ ],
                searchInputVal:[ ],
                homeSearchCondition : {
                    city_id : 1,
                    project_type : '',
                    doWhat : '',
                    q : {
                        site_site_type_eq : '',
                        keyword_cont : ''
                    }
                }
            }

        },
        computed: {
            searchCondition (){
                return this.$store.state.searchCondition
            },
            cityHotKeyword(){
                return this.$store.state.cityHotKeyword
            }
        },
        components: {},
        mounted () {
            $.noConflict();
            jQuery('.zy-Slide').zySlide({ speed: 500 }).css('border', '0px solid blue');

            var self = this;

            self.$store.commit('loading',true);

            $.ajax({
                url: window.YUNAPI.openShop,
                data : {
                    city_id : self.$store.state.city_id
                },
                success: function (data) {
                    self.specials=data.retail_special;
                    self.topLists=data.retail_top_list;
                    self.recommendSpace=data.retail_recommend_space;
                    self.selectedCase=data.retail_selected_case;

                    self.$store.commit('loading',false);
                }
            });

        },
        methods: {
            //搜索点击跳转到空间列表页
            getSearchVal:function () {
                this.searchInputVal=$('.searchInputVal').val();
                window.location.href ='/spacelist/:'+this.searchInputVal;
            },
            goSpaceSearch :function () {
                this.$store.commit('spaceSearchCondition', this.homeSearchCondition);
                router.push('/spaces');
            },
            spaceSearchFixed(e){
                this.homeSearchCondition.q.keyword = e
                this.$store.commit('spaceSearchCondition', this.homeSearchCondition);
                router.push('/spaces');
            },
            spaceSearchTypeFixed(e){
                this.homeSearchCondition.q.site_site_type_eq = e
                this.$store.commit('spaceSearchCondition', this.homeSearchCondition);
                router.push('/spaces');
            }
        },

    }
</script>





