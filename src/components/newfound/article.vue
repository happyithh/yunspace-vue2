<template>
    <div class="w1200 newfound clearfix">
        <!--左边文章列表-开始-->
        <div class="fl left clearfix">
            <div class="s-wrap clearfix">
                <ul class="fl selectlist clearfix">
                    <li :class="selectType == '' ? 'active' : '' " v-on:click="clearType">全部</li>
                    <li :class="selectType == 'newsType' ? 'active' : '' ">
                        <!--资讯-->
                        <el-select v-model="newsType"  v-on:change = 'newsTypeChange' placeholder="资讯">
                            <el-option
                                    v-for="(value,key) in articleType['资讯']"
                                    :label="key"
                                    :value="value">
                            </el-option>
                        </el-select>
                    </li>

                    <li :class="selectType == 'guideType' ? 'active' : '' ">
                        <!--攻略-->
                        <el-select v-model="guideType" v-on:change = 'guideTypeChange' placeholder="攻略">
                            <el-option
                                    v-for="(value,key) in articleType['攻略']"
                                    :label="key"
                                    :value="value">
                            </el-option>
                        </el-select>
                    </li>

                    <li :class="selectType == 'caseType' ? 'active' : '' ">
                        <!--案例-->
                        <el-select v-model="caseType" v-on:change = 'caseTypeChange' placeholder="案例">
                            <el-option
                                    v-for="(value,key) in articleType['案例']"
                                    :label="key"
                                    :value="value">
                            </el-option>
                        </el-select>
                    </li>
                </ul>
                <!--selectlist-end-->
                <div class="fl search-warp clearfix">
                    <input class="fl" type="text" v-model="searchKeyword" placeholder="输入关键字" v-on:keypress = 'searchSubmit'>
                    <button class="fr searchbtn" v-on:click="bindGetArticle">搜索</button>
                </div>
            </div>

            <div class="article-wrap">
                <ul>
                    <li class="clearfix" v-for="item in articles">
                        <div class="fl img">
                            <a target="_blank" v-bind:href="item.special_url ? item.special_url : '/article/' + item.id">
                                <img onerror="javascript:this.src='/static/images/error.jpg';" v-bind:src="item.img_paths.length > 0 ? item.img_paths[0]['url_400_267'] : ''"></a>
                            <span class="tag red">{{item.i_type_name}}</span>
                        </div>
                        <div class="fr text">

                            <a target="_blank" class="title" v-bind:href="item.special_url ? item.special_url : '/article/' + item.id">{{item.title}}</a>

                            <p>{{item.abstract}}</p>
                            <div class="numb-time clearfix">
                                <p class="fl">{{item.created_at}}</p>
                                <ul class="fr numbs clearfix">
                                    <li class="fl"><i class="icons icon-skim"></i>{{item.viewed}}</li>
                                    <li v-if="item.special_url ? false : true" class="fr"><i class="icons icon-zan"></i>{{item.up_number}}</li>
                                </ul>
                            </div>
                        </div>
                    </li>
                </ul>
                <span id="moreArticle" v-if="!isNoMoreData" class="more" href="javascript:;" @click="moreArticle">
                    <span>加载更多</span>
                    <i class="icon-arrowbottom"></i>
                </span>
                <p style="text-align: center" v-if="articles.length <= 0">暂无相关文章</p>
            </div><!--article-wrap-end-->
        </div>
        <!--左边文章列表-结束-->

        <div class="fr right">
            <div class="tags clearfix">
                <!--<router-link :to="'/found?keyword='+item" v-for="item in tags">{{item}}</router-link>-->
                <a v-for="item in tags" href="javascript:;" @click="keywordClick(item)">{{item}}</a>
                <!--<a href="javascript:;">媒体新闻</a>-->
                <!--<a href="javascript:;">市集地摊</a>-->
                <!--<a href="javascript:;">文体娱乐</a>-->
                <!--<a href="javascript:;">媒体新闻</a>-->
                <!--<a href="javascript:;">市集地摊</a>-->
                <!--<a href="javascript:;">文体娱乐</a>-->
                <!--<a href="javascript:;">媒体新闻</a>-->
            </div>

            <div class="hot-recommend">
                <h2>热门推荐</h2>
                <ul>
                    <li class="clearfix" v-for="item in hotArticle">
                        <div class="fl img">
                            <a target="_blank" :href="item.special_url ? item.special_url : '/article/' + item.id"><img v-bind:src="item.img_paths.length > 0 ? item.img_paths[0]['url_400_267'] : ''"></a>
                        </div>
                        <div class="fr text">
                            <a class="title" target="_blank" :href="item.special_url ? item.special_url : '/article/' + item.id">{{item.title}}</a>
                            <p class="time">{{item.created_at}}</p>
                        </div>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>

    import Lib from 'assets/Lib.js'
    import Owl from 'assets/owl.js'

    import 'assets/css/component.css';
    import 'assets/css/newfound.css';

    import moduleHeader from 'components/module-header';
    import moduleFooter from 'components/module-footer';

    export default{
        data(){
            return {
                newsType: '',
                guideType : '',
                caseType : '',
                articles:[],
                articleTags : [],
                articleType : [],
                recommends:[1,2,3,4,5,6],
                selectType : '',
                selectTypeKey : '', // 文章类型
                searchKeyword : '', // 搜索关键词
                hotArticle : [], //热门文章
                tags : [],
                isNoMoreData : false,
                isGetData : ''
            }
        },

        computed: {
//            newsType (){
//                return this.$route.query.newsType * 1
//            }
        },
        watch: {
            // 如果路由有变化，会再次执行该方法
            '$route': 'reload'
        },
        created(){

        },
        mounted(){
            var self= this;

            setTimeout(function () {
                if(self.$route.query.newsType){
                    self.newsType = self.$route.query.newsType * 1
                }
                if(self.$route.query.caseType){
                    self.caseType = self.$route.query.caseType * 1
                }

//            console.log(typeof this.$route.query.newsType)
//            this.newsType = this.$route.query.newsType * 1
//            this.caseType = this.$route.query.caseType * 1
                if(self.$route.query.selectTypeKey){
                    self.selectTypeKey = self.$route.query.selectTypeKey * 1
                }

                if(self.$route.query.selectType){
                    self.selectType = self.$route.query.selectType
                }
            },300)

            if(!this.$route.query.caseType && !this.$route.query.newsType){
                this.getArticle() // 请求文章列表
            }

            self.$store.commit('loading',true);

            if(typeof this.$route.query.keyword != 'undefined'){
                self.searchKeyword = this.$route.query.keyword
            }else{
                self.searchKeyword = ''
            }

            $.ajax({
                url: window.YUNAPI.articleTags,
                success: function (data) {
//                    self.cities = data.cities;
                    self.articleTags = data;
//                    console.log(data);
                    self.articleType = data.information_type;
//                    self.newsType = 1;
//                    self.guideType = 23;
//                    self.caseType = 6;
                    self.selectType = '';

                },
                error : function () {
//                    console.log('error'.window.YUNAPI.articleTags)
                }
            });

            $.ajax({
                url: window.YUNAPI.articleHot,
                data : {
                    city_id : self.$store.state.city_id
                },
                success: function (data) {
                    //console.log(data)
                    self.hotArticle = data.hot_recommend;
                },
                error : function () {
//                    console.log('error'.window.YUNAPI.articleHot)
                }
            });

            //推荐标签
            $.ajax({
                url: window.YUNAPI.articleKeyword,
                success: function (data) {
                    self.tags = data.data;
                }
            });

        },
        methods: {
            newsTypeChange : function (e) {
                this.selectType = "newsType";
                this.selectTypeKey = e;
                this.getArticle();
            },
            guideTypeChange : function (e) {
                this.selectType = "guideType";
                this.selectTypeKey = e;
                this.getArticle();
            },
            caseTypeChange : function (e) {
                this.selectType = "caseType";
                this.selectTypeKey = e;
                this.getArticle();
            },
            searchSubmit : function () {
                if(event.keyCode==13){
                    this.getArticle();
                }
            },
            clearType : function () {
                var self = this;
                this.selectTypeKey = '';

                this.newsType =  ''
                this.guideType =  ''
                this.caseType =  ''

                setTimeout(function () {
                    self.selectType = '';
                },300)

                this.getArticle();
            },
            moreArticle : function () {
                var lastId = this.articles[this.articles.length - 1].id;
                this.getArticle(lastId,'more');
            },
            bindGetArticle : function () {
                this.getArticle();
            },
            getArticle : function (id,method) { //请求 文章列表
                if( this.articlePromise && this.articlePromise.state() == 'pending'){
                    return
                }
                var self= this;
                var urlData = {
                    page : 1,
                    i_keyword : self.searchKeyword,
                    i_class : '',
                    i_type : self.selectTypeKey,
                    i_id : id || ''
                };

                $('#moreArticle span').text('正在加载...')
                this.articlePromise = $.ajax({
                    url: window.YUNAPI.article,
                    context: document.body,
                    data : urlData,
                    success: function (data) {
//                    self.cities = data.cities;
//                        console.log(data)
                        if(method == 'more'){
                            self.articles = self.articles.concat(data.informations);
                        }else{
                            self.articles = data.informations;
                        }

                        if(data.informations.length < self.$store.state.pageSize){
                            self.isNoMoreData = true
                        }else{
                            self.isNoMoreData = false
                        }

                        self.$store.commit('loading',false);
                        $('#moreArticle span').text('加载更多')
                    },
                    error: function (data) {
                        $('#moreArticle span').text('加载更多')
                    }
                });
            },
            reload(){
                this.getArticle()
            },
            keywordClick(keyword){
                this.searchKeyword = keyword
                this.getArticle()
            }

        }

    }
</script>
