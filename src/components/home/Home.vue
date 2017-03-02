<template>
    <div class="home">
        <!--home-banner板块-开始-->
        <div class="home-banner-search">
            <!--home-banner部分-->
            <div class="home-banner-wrap">
                <div class="home-banner">
                    <img src="/static/images/home/home_banner.jpg">
                </div>
                <div class="banner_text">
                    <p>快速提交需求<span>&gt;</span></p>
                    <p>及时获得报价<span>&gt;</span></p>
                    <p>顾问预约看场<span>&gt;</span></p>
                    <p>签订场地合同<span>&gt;</span></p>
                    <p>顺利举办活动</p>
                </div>
            </div>
            <!--搜索-->
            <div class="home-search clearfix">
                <!--城市选择-->
                <div class="fl select city">
                    <div class="result">
                        <!--<input type="text" value="" placeholder="在哪个城市">-->
                        <!--<i class="icon-updown"></i>-->
                        <el-select v-model="homeSearchCondition.city_id">
                            <el-option
                                    v-for="item in searchCondition.cities"
                                    :label="item.name"
                                    :value="item.id">
                            </el-option>
                        </el-select>
                    </div>
                </div>
                <!--城市选择-结束-->

                <!--做什么-->
                <div class="fl select ml10 dowhat"  id="whatToSearch">
                    <div class="result" v-on:click="whatToSearchInputClick">
                        <input type="text" disabled value="" placeholder="做什么" v-model="homeSearchCondition.doWhat">
                        <i class="el-input__icon el-icon-caret-bottom"></i>
                    </div>
                    <div class="cont dowhat-contlist" v-show="this.$parent.$data.isShowHomeSearchCondition" id="whatToSearchContent">
                        <dl class="clearfix">
                            <dt class="fl">办活动</dt>
                            <dd class="fl">
                                <a :class=" homeSearchCondition.doWhat ==  key ? 'active' : ''" @click="searchConditionSelect(1,value,key)" href="javascript:;" v-for="(value,key) in searchCondition.space_type">{{key}}</a>
                                <!--<a href="javascript:;">商业发布</a>-->
                            </dd>
                        </dl>
                        <dl class="clearfix">
                            <dt class="fl">要开店</dt>
                            <dd class="fl">
                                <a :class=" homeSearchCondition.q.preKeyword ==  key ? 'active' : ''" @click="searchConditionSelect(2,key,key)" href="javascript:;" v-for="(key,value) in searchCondition.retail">{{key}}</a>
                                <!--<a href="javascript:;">店中店</a>-->
                            </dd>
                        </dl>
                        <dl class="clearfix">
                            <dt class="fl">IP项目</dt>
                            <dd class="fl">
                                <a @click="searchConditionSelect(3,key,value)" href="javascript:;" v-for="(key,value) in searchCondition.project_type">{{value}}</a>
                                <!--<a href="javascript:;">卡通</a>-->
                            </dd>
                        </dl>
                    </div>
                </div>
                <!--做什么-结束-->

                <!--搜索-->
                <input @keyup.enter="homeDoSearch" v-model="homeSearchCondition.q.keyword" class="fl ml10 searchinput" type="text" placeholder="商圈／地标／机场／火车站／场地名">
                <button class="fl ml20 searchbtn" @click="homeDoSearch">搜 索</button>
                <div class="fr onekeyorder clearfix">
                    <span class="fl">或</span>
                    <button class="fr onekeybtn" @click="oneKey">一键租场地</button>
                </div>
            </div>
        </div>
        <!--home-banner板块-结束-->

        <!--快捷链接块-开始-->
        <ul class="quicklinks clearfix">
            <li>
                <router-link to="/event" class="imgtext">
                    <img src="/static/images/home/links1.jpg">
                    <p class="text">本月新增场地92家</p>
                    <div class="mask"></div>
                </router-link>
                <!--<p class="imgtitle">我要办活动</p>-->
                <router-link class="imgtitle" to="/event">我要办活动</router-link>
            </li>
            <li>
                <router-link to="/openshop" class="imgtext">
                    <img src="/static/images/home/links2.jpg">
                    <p class="text">本月新增空间345家</p>
                    <div class="mask"></div>
                </router-link>
                <!--<p class="imgtitle">我要开店</p>-->
                <router-link class="imgtitle" to="/openshop">我要开店</router-link>
            </li>
            <li>
                <router-link to="/ip" class="imgtext">
                    <img src="/static/images/home/links3.jpg">
                    <p class="text">本月新增项目5个</p>
                    <div class="mask"></div>
                </router-link>
                <!--<p class="imgtitle">我要找IP项目</p>-->
                <router-link class="imgtitle" to="/ip">我要找IP项目</router-link>
            </li>
        </ul>

        <!--城市精选专题-开始-->
        <div class="section citysubject clearfix">
            <div class="w1200">
                <h3>城市精选专题</h3>
                <div class="cont">
                    <div class="btns">
                        <a class="btn btnleft" href="javascript:;">
                            <span class="icon-arrowleft"></span>
                        </a>
                        <a class="btn btnright" href="javascript:;">
                            <span class="icon-arrowright"></span>
                        </a>
                    </div>
                    <div class="citySelection" style="height: 100%;">
                        <div class="swiper-wrapper swiper-container">
                            <div class="swiper-slide" v-for="item in topicOfCity">
                                <a :href="item.special_url ? item.special_url : '/article/' + item.id" target="_blank">
                                    <img :src="item.img_paths.length > 0 ? item.img_paths[0]['url_400_267'] : ''" alt="">
                                    <p>{{item.title}}</p>
                                </a>
                            </div>
                            <!--<div class="swiper-slide">Slide 2</div>-->
                            <!--<div class="swiper-slide">Slide 3</div>-->
                            <!--<div class="swiper-slide">Slide 4</div>-->

                        </div>
                        <!-- Add Pagination -->
                        <!--<div class="swiper-pagination"></div>-->
                    </div>
                    <ul class="subject-list"></ul>
                </div>
                <router-link to="/found" class="btnlookmore">查看更多专题</router-link>
                <!--<a href="javascript:;" class="btnlookmore">查看更多专题</a>-->
            </div>

        </div>
        <!--城市精选专题-结束-->

        <!--&lt;!&ndash;分类精选-开始&ndash;&gt;-->
        <!--<div class="section classifyselected clearfix">-->
            <!--<h3>分类精选</h3>-->
            <!--<ul class="cont clearfix">-->
                <!--<li v-for="(item,index) in typeSelected" @click="spaceSearchTypeFixed(item[0].space_type)"  v-if="index < 3">-->
                    <!--<a class="imgnumb" href="javascript:;">-->
                        <!--<img :src="'http://106.14.38.81/'+item[0].logo">-->
                        <!--&lt;!&ndash;<div class="mask"></div>&ndash;&gt;-->
                    <!--</a>-->
                    <!--<p class="numb">{{item[0].count}}</p>-->
                    <!--<p class="imgtitle">{{item[0].name}}</p>-->
                <!--</li>-->
                <!--<li v-for="(item,index) in typeSelected" @click="spaceSearchKeywordFixed(item[0].name)"  v-if="index >= 3">-->
                    <!--<a class="imgnumb" href="javascript:;">-->
                        <!--<img :src="'http://106.14.38.81/'+item[0].logo">-->
                        <!--&lt;!&ndash;<div class="mask"></div>&ndash;&gt;-->
                    <!--</a>-->
                    <!--<p class="numb">{{item[0].count}}</p>-->
                    <!--<p class="imgtitle">{{item[0].name}}</p>-->
                <!--</li>-->
                <!--&lt;!&ndash;<li>&ndash;&gt;-->
                <!--&lt;!&ndash;<a class="imgnumb" href="javascript:;">&ndash;&gt;-->
                <!--&lt;!&ndash;<img src="/static/images/home/links1.png">&ndash;&gt;-->
                <!--&lt;!&ndash;<div class="mask"></div>&ndash;&gt;-->
                <!--&lt;!&ndash;</a>&ndash;&gt;-->
                <!--&lt;!&ndash;<p class="numb">255</p>&ndash;&gt;-->
                <!--&lt;!&ndash;<p class="imgtitle">场馆</p>&ndash;&gt;-->
                <!--&lt;!&ndash;</li>&ndash;&gt;-->
            <!--</ul>-->
        <!--</div>-->
        <!--&lt;!&ndash;分类精选-结束&ndash;&gt;-->

        <!--空间推荐-开始-->
        <div class="section spacerecommend clearfix">
            <h3>空间推荐</h3>
            <ul class="recommend recommend-main clearfix">
                <li v-for="(item,index) in spaceRecommend" v-if="index < 3">
                    <div class="img">
                        <a :href=" '/space/' + item.id" target="_blank">
                            <img v-bind:src="item.img_paths.length > 0 ? item.img_paths[0]['url_400_267'] : '' ">

                        </a>
                        <span class="tags">{{item.city_name}}</span>
                    </div>
                    <div class="text">
                        <a target="_blank" class="title" :href=" '/space/' + item.id">{{item.name}}</a>
                        <div class="price">{{item.special_price}}</div>
                        <div class="textinfo">
                            <p><span>场地类型：</span>{{item.site_type}}</p>
                            <p><span>落地区域：</span>{{item.through_three_areas}}</p>
                            <div class="numb clearfix">
                                <p><span>面积：</span>{{item.area}}㎡</p>
                                <p><span>层高：</span>{{item.height}}m</p>
                                <p><span>人数：</span>{{item.Max_seating_capacity}}人</p>
                            </div>
                            <p><span>地址：</span>{{item.city_name}} | {{item.district}} | {{item.address}}</p>
                        </div>
                    </div>
                </li>
            </ul>
            <ul class="recommend recommend-sub clearfix">
                <li v-for="(item,index) in spaceRecommend" v-if=" index >=3">
                    <div class="img">
                        <a :href=" '/space/' + item.id" target="_blank">
                            <img v-bind:src="item.img_paths.length > 0 ? item.img_paths[0]['url_400_267'] : ''">
                        </a>
                    </div>
                    <div class="text">
                        <a class="title" target="_blank" :href=" '/space/' + item.id">{{item.name}}</a>
                        <div class="price">{{item.special_price}}</div>
                        <div class="city">{{item.city_name}}</div>
                        <div class="textinfo">
                            <p><span>场地类型：</span>{{item.site_type}}</p>
                            <p><span>落地区域：</span>{{item.through_three_areas}}</p>
                            <p><span>地址：</span>{{item.city_name}} | {{item.district}} | {{item.address}}</p>
                        </div>
                    </div>
                </li>
            </ul>
            <ul class="recommend-other"></ul>

            <router-link class="btnlookmore" to="/spaces">查看更多空间</router-link>
            <!--<a class="btnlookmore" href="javascript:;">查看更多空间</a>-->
        </div>
        <!--空间推荐-结束-->

        <!--ip文创项目-开始-->
        <div class="section ipwinchuang clearfix">
            <h3>IP文创项目</h3>
            <ul class="cont clearfix">
                <li class="clearfix" v-for="item in ipProject">
                    <a class="maskbtn" href="javascript:;" @click.native="consultClick(item.id)">
                        <!--<p  @click.native="consultClick(item.id)">合作咨询</p>-->
                        <el-button class="op-coop" type="text"  @click.native="consultClick(item.id,item.title)">合作咨询</el-button>
                    </a>
                    <div class="img">
                        <img v-bind:src="item.img_paths.length > 0 ? item.img_paths[0]['url_400_267'] : ''">
                    </div>
                    <div class="textinfo">
                        <div class="title">{{item.title}}</div>
                        <p class="tags">
                            <span v-for="i in item.keywords">{{i}}</span>
                        </p>
                        <div class="group clearfix">
                            <p>类别：{{item.p_type}}</p>
                            <p>来源：{{item.source}}</p>
                        </div>
                        <p>场地面积：{{item.area}} m²</p>
                        <!--MARK无对应字段-->
                        <p>适用人群：冰川时代影迷</p>
                        <p>预算范围：{{item.budget_amount}}</p>
                    </div>
                </li>
            </ul>
            <router-link class="btnlookmore" to="/iplist">查看更多项目</router-link>
        </div>
        <!--ip文创项目-结束-->

        <!--场地配套服务-开始-->
        <!--<div class="section ipwinchuang clearfix">-->
        <!--<h3>场地配套服务</h3>-->
        <!--<div class="cont">-->
        <!--<div class="btns">-->
        <!--<a class="btn btnleft" href="javascript:;">-->
        <!--<span class="icon-arrowleft"></span>-->
        <!--</a>-->
        <!--<a class="btn btnright" href="javascript:;">-->
        <!--<span class="icon-arrowright"></span>-->
        <!--</a>-->
        <!--</div>-->

        <!--<ul class="iplist"></ul>-->
        <!--</div>-->

        <!--</div>-->
        <!--场地配套服务-结束-->

        <!--新发现-开始-->
        <div class="section newfound clearfix">
            <h3>新发现</h3>
            <div class="cont clearfix">
                <!--大图那个-->
                <div class="fl info info-big" v-for="(item,index) in newFindTopFour" v-if="index < 1">
                    <a class="img" :href=" '/article/' + item.id" target="_blank">
                        <img :src="item.img_paths.length > 0 ? item.img_paths[0]['url_400_400'] : ''">
                    </a>
                    <a class="text" :href=" '/article/' + item.id" target="_blank">
                        {{item.title}}
                    </a>
                </div>
                <!--中间4个-->
                <ul class="infolist fl clearfix">
                    <li class="info info-normal" v-for="(item,index) in newFindTopFour" v-if="index > 0">
                        <a class="img" :href="'/article/' + item.id" target="_blank">
                            <img v-bind:src="item.img_paths.length > 0 ? item.img_paths[0]['url_400_267'] : ''">
                        </a>
                        <a class="text" :href="'/article/' + item.id" target="_blank">
                            {{item.title}}
                        </a>
                    </li>
                </ul>
                <!--右边列表-->
                <ul class="fr textinfolist clearfix">

                    <li v-for="item in newFindRandom">
                        <a :href="'/article/' + item.id" target="_blank">
                            <div class="title">
                                <i class="point"></i>
                                <p>{{item.title}}</p>
                            </div>
                            <p>{{item.abstract}}</p>
                        </a>
                    </li>

                </ul>
            </div>
            <!--<a class="btnlookmore" href="javascript:;">发现更多精彩</a>-->
            <router-link class="btnlookmore" to="/found?newsType=1&selectType=newsType&selectTypeKey=1">发现更多精彩</router-link>
        </div>
        <!--新发现-结束-->

        <!--精选案例-开始-->
        <div class="section caseselected clearfix">
            <h3>精选案例</h3>
            <ul class="cont clearfix">
                <li v-for="item in caseSelected">
                    <a :href="'/article/' + item.id" target="_blank" class="img">
                        <img v-bind:src="item.img_paths.length > 0 ? item.img_paths[0]['url_400_267'] : ''">
                    </a>
                    <div class="textinfo">
                        <a class="title" :href="'/article/' + item.id" target="_blank">{{item.title}}</a>
                        <div class="tags">
                            <span v-for="(i,index) in item.keywords" v-if="index < 3">{{i}}</span>
                        </div>
                        <ul class="numbs clearfix">
                            <li class="fl"><i class="icons icon-skimbg"></i>{{item.viewed}}</li>
                            <li class="fr"><i class="icons icon-zanbg"></i>{{item.up_number}}</li>
                        </ul>
                    </div>
                </li>
            </ul>
            <router-link class="btnlookmore" to="/found?caseType=6&selectType=caseType&selectTypeKey=6">发现更多案例</router-link>
            <!--<a class="btnlookmore" href="javascript:;">发现更多精彩</a>-->
        </div>
        <!--精选案例-开始-->

        <!--媒体报道-开始-->
        <div class="section mediacoverage clearfix">
            <h3>媒体报道</h3>
            <div class="cont media-wrap clearfix">
                <!--<div class="fl imglogo-media">-->
                    <!--<img src="/static/images/home/imglogo-media.png">-->
                <!--</div>-->
                <ul class="textinfolist clearfix media">
                    <li v-for="(item,index) in mediaReport" v-if="index < 5">
                        <router-link :to="'/article/'+item.id">
                            <div class="title fl">
                                <i class="point"></i>
                                <p>{{item.title}}</p>
                            </div>
                            <div class="time fr">{{item.i_time}}</div>
                        </router-link>
                    </li>
                    <!--<li>-->
                    <!--<a href="javascript:;">-->
                    <!--<div class="title">-->
                    <!--<i class="point"></i>-->
                    <!--<p>[网易] 商业地产短租入侵零售领域 云SPACE掀起商业场景革命</p>-->
                    <!--</div>-->
                    <!--<div class="time">2016-08-15</div>-->
                    <!--</a>-->
                    <!--</li>-->

                </ul>
                <ul class="textinfolist clearfix media">
                    <li v-for="(item,index) in mediaReport" v-if="index >= 5">
                        <router-link :to="'/article/'+item.id">
                            <div class="title fl">
                                <i class="point"></i>
                                <p>{{item.title}}</p>
                            </div>
                            <div class="time fr">{{item.i_time}}</div>
                        </router-link>
                    </li>
                    <!--<li>-->
                    <!--<a href="javascript:;">-->
                    <!--<div class="title">-->
                    <!--<i class="point"></i>-->
                    <!--<p>[网易] 商业地产短租入侵零售领域 云SPACE掀起商业场景革命</p>-->
                    <!--</div>-->
                    <!--<div class="time">2016-08-15</div>-->
                    <!--</a>-->
                    <!--</li>-->

                </ul>
            </div>
        </div>
        <!--媒体报道-开始-->

        <!--媒体报道-开始-->
        <div class="section logofriends clearfix">
            <h3>合作品牌</h3>
            <div class="cont">
                <img src="/static/images/home/imglogo-friends.png">
            </div>
        </div>
        <consult-form ref="consult"></consult-form>
    </div>

</template>

<script>

    import Lib from 'assets/Lib.js';
    import 'assets/libs/swiper/swiper.js'

    require ('assets/css/component.css');
    import consultForm from '../../components/ip/consultForm';
    //    require ('assets/css/home.css');
    export default {
        data(){
            return {
                spacemains: [
                    1, 2, 3
                ],
                spacesubs: [
                    1, 2, 3, 4
                ],
                ipinfos: [
                    1, 2, 3, 4
                ],
                cases: [
                    1, 2, 3, 4, 5, 6
                ],
                options: [{
                    value: '选项1',
                    label: '黄金糕'
                }, {
                    value: '选项2',
                    label: '双皮奶'
                }, {
                    value: '选项3',
                    label: '蚵仔煎'
                }, {
                    value: '选项4',
                    label: '龙须面'
                }, {
                    value: '选项5',
                    label: '北京烤鸭'
                }],
                searchCity: 1,
                showdowhat: 0,

                ipProject : [],
                topicOfCity : [], // 城市精选专题
                newFindTopFour : [], // 新发现左边
                newFindRandom : [], // 新发现右边
                newFindFirst : {},
                typeSelected : [], //分类精选
                spaceRecommend : [], //空间推荐
                caseSelected : [], //精选案例
                mediaReport : [], //媒体,

                homeSearchCondition : {
                    city_id : 1,
                    project_type : '',
                    doWhat : '',
                    q : {
                        site_site_type_eq : '',
                        keyword : '',
                        preKeyword : ''
                    }
                }
            }
        },
        computed : {
            searchCondition (){
                return this.$store.state.searchCondition
            },

//            spaceSearchCondition () {
//                return this.$store.state.spaceSearchCondition
//            }
        },
        created(){
            var self = this
            window.bus.$off('city-selected')
            window.bus.$on('city-selected', function (id) {
                self.componentInit(id)
            })
        },
        components: {
            consultForm
        },
        mounted () {
            var self = this;
            self.componentInit()
        },
        methods: {
            componentInit(id){
                var self = this;
                self.$store.commit('loading',true); //显示loading 状态
                $.ajax({
                    url: window.YUNAPI.home, data : {
                        city_id : self.$store.state.city_id
                    }, success: function (data) {

//                        console.log(data)

                        self.$store.commit('loading',false);

                        self.topicOfCity = data.home_city_special;
                        self.newFindTop = data.home_new_find_top;
                        self.newFindRandom = data.home_new_find_random;
                        self.spaceRecommend = data.home_recommend_space;

//                    self.caseSelected = data.home_case_selected;

                        // 关键词 需要按,分割
                        for (var i = 0; i <  data.home_case_selected.length; i++){
                            data.home_case_selected[i].keywords = []
                            if(data.home_case_selected[i].keyword){
                                data.home_case_selected[i].keywords = data.home_case_selected[i].keyword.split(',')
                            }

                        }
                        self.caseSelected = data.home_case_selected;

                        //ip项目 关键词
                        for(var i = 0; i <  data.home_project.length; i++){
                            data.home_project[i].keywords = []
                            if(data.home_project[i].keyword){
                                data.home_project[i].keywords = data.home_project[i].keyword.split(',')
                            }
                        }
                        self.ipProject = data.home_project;

//                    self.typeSelected = data.home_type_selected_by_retail.concat(data.home_type_selected_by_space);


                        self.newFindTopFour = data.home_new_find_top; // 新发现4个
//                    self.newFindFirst = self.newFindTopFour.shift(); //新发现第一个

                        self.mediaReport = data.home_media;

                        self.typeSelected = data.home_type_selected

//                    console.log(self.spaceRecommend);
//                    console.log(self.newFindRandom);

                        setTimeout(function () {
                            self.init();
                        },300)
                    }
                });
            },
            whatToSearchInputClick : function () {
                this.$parent.$data.isShowHomeSearchCondition = !this.$parent.$data.isShowHomeSearchCondition
            },
            init : function () {

                var citySelectionSwiper = new Swiper('.citySelection', {
//                    pagination: '.swiper-pagination',
                    nextButton: '.citysubject .btnright',
                    prevButton: '.citysubject .btnleft',
                    loop : true,
                    slidesPerView: 3,
                    paginationClickable: true,
                    spaceBetween: 1,
                    autoplay: 3000
//                    freeMode: true
                });
            },
            searchConditionSelect : function (type,key,value) {
                var self = this;
//                console.log(type,key,value)
                if(type == 1){
                    self.homeSearchCondition.q.site_site_type_eq = key
                }
                if(type == 2){
                    self.homeSearchCondition.q.preKeyword = key
                }
                if(type == 3){
//                    self.homeSearchCondition.project_type = key
                    self.homeSearchCondition.project_type = key
                }
                self.homeSearchCondition.doWhat = value;
                self.$parent.isShowHomeSearchCondition = false
            },
            homeDoSearch : function () {
                if(this.homeSearchCondition.q.preKeyword){
                    this.homeSearchCondition.q.keyword = this.homeSearchCondition.q.preKeyword + ' ' + this.homeSearchCondition.q.keyword
                }
                this.$store.commit('spaceSearchCondition', this.homeSearchCondition);
                router.push('/spaces');
            },
            consultClick : function (id,title) {
                this.$refs.consult.consult.title = title;
                this.$refs.consult.consult.project_id = id;
                this.$refs.consult.cdVisible = true;
            },
            spaceSearchKeywordFixed(e){
                this.homeSearchCondition.q.keyword = e
                this.$store.commit('spaceSearchCondition', this.homeSearchCondition);
                router.push('/spaces');
            },
            spaceSearchTypeFixed(e){
                this.homeSearchCondition.q.site_site_type_eq = e
                this.$store.commit('spaceSearchCondition', this.homeSearchCondition);
                router.push('/spaces');
            },
            oneKey(){
                router.push('/event/hold?type=onekey')
            }

        }
    }
</script>
<style scoped>
    .citySelection .swiper-slide{
        background-color: #fff;
        /*height: 350px;*/
        margin-right: 1px;
        position: relative;
    }
    .swiper-container{
        overflow: visible;
    }
    .citySelection .swiper-slide a{
        display: block;
        width: 100%;
        height: 100%;
    }
    .citySelection .swiper-slide a:after{
        content: '';
        display: block;
        width: 100%;
        height: 100%;
        background: rgba(0,0,0,.3);
        position: absolute;
        left: 0;
        top: 0;
        z-index: 1;
    }
    .citySelection .swiper-slide img{
        display: block;
        width: 100%;
        height: 100%;
        background: #aaa;
    }
    .citySelection .swiper-slide p{
        position: absolute;
        bottom: 0;
        z-index: 2;
        font-size:18px;
        color:#ffffff;
        margin: 10px 15px;
        height: 46px;
        line-height: 1.35em;
        box-sizing: border-box;
        overflow: hidden;

        display: -webkit-box;  /*将对象作为弹性盒子模型显示*/
        text-overflow:ellipsis;
        word-break:break-all;
        -webkit-box-orient:vertical;/*伸缩盒对象的子元素的排列方式-垂直*/
        -webkit-line-clamp:2; /*限制在一个块级元素显示的文本的行数*/

        transition: all .6s;
        -webkit-transition: all .6s;
        -moz-transition: all .6s;
    }
    .citySelection .swiper-slide:hover p{
        bottom: 5px;
    }
    /*.citySelection{*/
    /*width: 1200px;*/
    /*}*/

    .btnlookmore {
        display: block;
        width: 398px;
        height: 48px;
        line-height: 48px;
        border: 1px solid #000;
        text-align: center;
        margin: 30px auto 0;
        font-size: 18px;
        color: #000;
        background: #fff;
    }

    .btnlookmore:hover {
        background: #000;
        color: #fff;
    }

    .section {
        width: 1200px;
        margin: 0 auto 50px;
    }

    .section > h3 {
        font-size: 24px;
        margin-bottom: 30px;
        height: 24px;
        line-height: 24px;
    }
    .home-banner-search{
        position: relative;
        min-width: 1200px;
        z-index: 10;
    }
    .home-banner-wrap{
        width: 100%;
        min-width: 1200px;
        height: 400px;
        margin: 0 auto;
        background: #ddd;
        overflow: hidden;
        position: relative;
    }

    .home-banner {
        width: 1920px;
        height: 400px;
        background: #ddd;
        position: absolute;
        left: 50%;
        margin-left: -960px;
        top: 0;
        overflow: hidden;
        z-index: 1;
    }
    .home-banner>img{width: 100%;height: 100%;}

    /*banner上的文字*/
    .banner_text{
        width: 1060px;
        margin: 0 auto;
        position: absolute;
        left: 50%;
        margin-left: -530px;
        top: 145px;
        z-index: 9;
    }
    .banner_text p{
        float: left;
        font-size: 28px;
        height: 28px;
        line-height: 28px;
        font-weight: normal;
        font-family: "PingFangHK-Regular","Open Sans", Arial, "Hiragino Sans GB", "Microsoft YaHei", "微软雅黑";
        /*font-family: PingFangHK-Thin;*/
        text-align:center;
        color: #fff;


    }
    .banner_text p.mycolor{
        color: #fff;
        animation:mycolor .5s;
        -moz-animation:mycolor .5s; /* Firefox */
        -webkit-animation:mycolor .5s; /* Safari and Chrome */
        -o-animation:mycolor .5s; /* Opera */
    }
    .banner_text p span{
        margin: 0 18px;
    }
    .banner_text p:nth-of-type(1){animation-delay: 1s;}
    .banner_text p:nth-of-type(2){animation-delay: 1.5s;}
    .banner_text p:nth-of-type(3){animation-delay: 2s;}
    .banner_text p:nth-of-type(4){animation-delay: 2.5s;}

    @keyframes mycolor
    {
        from {color: #ccc;}
        to {color: #fff;}
    }
    @-moz-keyframes mycolor /* Firefox */
    {
        from {color: #ccc;}
        to {color: #fff;}
    }
    @-webkit-keyframes mycolor /* Safari 和 Chrome */
    {
        from {color: #ccc;}
        to {color: #fff;}
    }
    @-o-keyframes mycolor /* Opera */
    {
        from {color: #ccc;}
        to {color: #fff;}
    }



    .home-search {
        width: 1100px;
        padding: 0 50px;
        position: absolute;
        bottom: 100px;
        left: 50%;
        margin-left: -600px;
        z-index: 2;
    }

    .home-search .select {
        position: relative;
    }

    .home-search .select:hover .result .icon-updown {
        transform: rotate(-180deg);
        -ms-transform: rotate(-180deg); /* IE 9 */
        -moz-transform: rotate(-180deg); /* Firefox */
        -webkit-transform: rotate(-180deg); /* Safari 和 Chrome */
        -o-transform: rotate(-180deg); /* Opera */
    }

    .home-search .select .cont {
        border:1px solid #272335;
        box-shadow:0px 2px 4px 0px rgba(0,0,0,0.50);
        position: absolute;
        left: 0;
        top: 52px
    }

    .home-search .result {
        width: 120px;
        height: 50px;
        background: #fff;
        position: relative;
        border: 1px solid #000;
        box-sizing: border-box;
    }

    .home-search .result input {
        width: 100%;
        height: 100%;
        line-height: 50px;
        cursor: pointer;
        background-color: #fff;
    }

    .home-search .result .icon-updown {
        display: block;
        width: 0px;
        height: 0px;
        border: 0;
        border-left: 5px solid transparent;
        border-right: 5px solid transparent;
        border-top: 7px solid #000;
        position: absolute;
        right: 22px;
        top: 21px;
        transition: all linear .2s;
    }
    body .home-search .el-input__inner{
        padding: 3px 20px;
    }
    body .home-search .el-input__icon{right: 19px;top:20px;}
    body .el-select-dropdown__item{
        padding: 8px 20px;
    }
    body .el-select-dropdown{
        margin: 2px 0;
    }
    body .el-select-dropdown__item.selected.hover,
    body .el-select-dropdown__item.selected{
        background: #e92332;
    }

    .citylist {
        width: 150px;
    }

    .citylist li {
        width: 100%;
        height: 30px;
        line-height: 30px;
    }

    .citylist li > a {
        width: 100%;
        height: 100%;
        background: #fff;
        text-indent: 20px;
    }

    .citylist li a:hover {
        background: #e92332;
        color: #fff;
    }
    .dowhat .result{
        padding: 0 20px;
        box-sizing: border-box;
        cursor: pointer;
    }
    .dowhat-contlist {
        width: 800px;
        background: #fff;
    }

    .dowhat-contlist dl {
        border-bottom: 2px solid #ccc;
        padding: 15px 20px;
    }

    .dowhat-contlist dl:last-child {
        border: 0;
    }

    .dowhat-contlist dt {
        width: 9%;
        height: 30px;
        line-height: 30px;
        margin: 5px 0;
    }

    .dowhat-contlist dd {
        width: 91%;
    }

    .dowhat-contlist dd > a {
        height: 30px;
        line-height: 30px;
        padding: 0 12px;
        margin: 5px;
    }

    .dowhat-contlist dd > a:hover,.dowhat-contlist dd > a.active {
        background: #e92332;
        color: #fff;
    }

    .searchinput {
        width: 500px;
        height: 50px;
        padding: 0 20px;
        border: 1px solid #000;
        box-sizing: border-box;
    }

    .searchbtn {
        width: 120px;
        height: 50px;
        line-height: 50px;
        text-align: center;
        color: #fff;
        font-size: 18px;
        background: #272335;
        cursor: pointer;
    }

    .searchbtn:hover {
        background: #1a152e;
    }
    .onekeyorder{
        width: 190px;
        height: 50px;
        line-height: 50px;
        font-size: 18px;
        color: #fff;
    }
    .onekeyorder .onekeybtn{
        background:rgba(255,255,255,0.3);
        border:2px solid #f4f4f4;
        width:160px;
        height: 100%;
        font-size: 18px;
        color: #fff;
    }

    /*快捷链接*/
    .quicklinks {
        width: 1000px;
        padding: 0 100px;
        margin: 40px auto;
    }

    .quicklinks li {
        float: left;
        width: 300px;
        height: 235px;
        margin-right: 50px;
    }

    .quicklinks li:last-child {
        margin-right: 0;
    }

    .quicklinks li a.imgtext {
        width: 100%;
        height: 200px;
        overflow: hidden;
        position: relative;
    }
    .quicklinks li a.imgtext img{
        transition: all 0.6s;
        -moz-animation: all 0.6s;
        -webkit-animation: all 0.6s;
        -o-animation: all 0.6s;
    }
    .quicklinks li a.imgtext:hover img{
        transform: scale(1.1,1.1);
        -moz-transform:scale(1.1,1.1);
        -webkit-transform:scale(1.1,1.1);
        -o-transform:scale(1.1,1.1);
    }

    .quicklinks li a.imgtitle{
        color: #000;
    }

    .quicklinks li .text {
        width: 100%;
        height: 24px;
        line-height: 24px;
        font-size: 24px;
        color: #fff;
        text-align: center;
        position: absolute;
        top: 50%;
        margin-top: -12px;
        z-index: 2;
    }

    li .mask {
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, .5);
        position: absolute;
        left: 0;
        top: 0;
        z-index: 1;

    }
    .classifyselected li .mask{
        border-radius: 50%;
    }

    li .imgtitle {
        width: 100%;
        height: 24px;
        line-height: 24px;
        text-align: center;
        margin-top: 10px;
        font-size: 24px;
    }

    /*城市精选专题*/

    /*分类精选*/
    .classifyselected li {
        float: left;
        width: 150px;
        height: 185px;
        margin-right: 55px;
        position: relative;
        cursor: pointer;
    }

    .classifyselected li:last-child {
        margin-right: 0;
    }

    .classifyselected li a {
        width: 150px;
        height: 150px;
        overflow: hidden;
        border-radius: 75px;
        position: relative;
    }

    .classifyselected li .numb {
        width: 60px;
        height: 60px;
        background: #000;
        line-height: 60px;
        border-radius: 30px;
        text-align: center;
        font-size: 18px;
        color: #fff;
        position: absolute;
        top: 45px;
        right: -30px;
        z-index: 2;
    }

    .classifyselected li .numb {
        transition: All 1s;
        -webkit-transition: All 1s;
        -moz-transition: All 1s;
        -o-transition: All 1s;
    }
    .classifyselected li:hover .numb {
        transform: scale(1.2);
        -webkit-transform: scale(1.2);
        -moz-transform: scale(1.2);
        -o-transform: scale(1.2);
        -ms-transform: scale(1.2);
    }

    /**小圆转一圈效果**/
    /*.classifyselected li:hover .numb {*/
    /*transform-origin: -82px 85px;*/
    /*-webkit-transform-origin: -82px 85px;*/

    /*transform: rotate(360deg);*/
    /*-webkit-transform: rotate(360deg);*/
    /*-moz-transform: rotate(360deg);*/
    /*-o-transform: rotate(360deg);*/
    /*-ms-transform: rotate(360deg);*/
    /*}*/

    .citysubject.section {
        width: 100%;
        min-width: 1200px;
        overflow: hidden
    }

    .citysubject h3 {
        width: 1200px;
        margin: 0 auto;
        font-size: 24px;
        height: 24px;
        line-height: 24px;
        margin-bottom: 30px;
    }

    .citysubject .cont {
        width: 100%;
        height: 235px;
        min-width: 1200px;
        overflow: hidden;
        position: relative;
    }

    /*空间推荐*/
    .recommend-main {
        margin-bottom: 20px;
    }

    .recommend-main li .tags {
        top: 10px;
    }

    .recommend-main .price {
        margin-bottom: 15px;
    }

    /*IP文创项目*/
    .ipwinchuang li {
        float: left;
        background: #fff;
        width: 595px;
        height: 200px;
        margin-right: 10px;
        margin-bottom: 10px;
        overflow: hidden;
        position: relative;
    }

    .ipwinchuang li:nth-child(2n+2) {
        margin-right: 0;
    }

    .ipwinchuang .maskbtn {
        width: 100%;
        height: 100%;
        background: rgba(255, 255, 255, .8);
        position: absolute;
        left: 0;
        bottom: -205px;
        /*opacity: 0;*/
        /*filter: alpha(opacity=0);*/
    }

    .ipwinchuang .maskbtn p,.ipwinchuang .maskbtn button {
        background: #272335;
        width: 120px;
        height: 40px;
        line-height: 40px;
        text-align: center;
        font-size: 18px;
        color: #fff;
        position: absolute;
        left: 50%;
        top: 50%;
        margin-left: -60px;
        margin-top: -20px;

    }

    .ipwinchuang li:hover .maskbtn {
        bottom: 0;
        /*opacity: 1;*/
        /*filter: alpha(opacity=100);*/
    }

    .ipwinchuang li .img {
        float: left;
        width: 300px;
        height: 200px;
        background: #ddd;
        overflow: hidden;
    }

    .ipwinchuang .textinfo {
        float: left;
        width: 275px;
        padding: 0 10px;
    }

    .ipwinchuang .textinfo .title {
        font-size: 18px;
        padding: 18px 0 13px;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
    }

    .ipwinchuang .textinfo .tags {
        margin-bottom: 10px;
    }

    .ipwinchuang .textinfo .tags span {
        margin-right: 20px;
    }

    .ipwinchuang .textinfo p {
        line-height: 24px;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
    }

    .ipwinchuang .textinfo .group p {
        float: left;
        margin-right: 20px;
    }

    /*场地配套服务*/
    .ipwinchuang .cont {
        position: relative;
    }

    /*新发现*/
    .newfound .info {
        background: #fff;
    }

    .newfound .info .img {
        background: #ddd;
        overflow: hidden;
    }

    .newfound .info-big {
        float: left;
        width: 377px;
        height: 419px;
    }

    .newfound .info-big .img {
        width: 378px;
        height: 350px;
        display: block;
    }

    .newfound .info-big .text {
        font-size: 18px;
        margin: 9px 15px;
        display: block;
        height: 48px;
        overflow: hidden;
    }

    .newfound .infolist {
        width: 420px;
    }

    .newfound .info-normal {
        float: left;
        width: 200px;
        height: 205px;
        margin: 0 0 10px 10px;
    }

    .newfound .info-normal .img {
        float: left;
        width: 100%;
        height: 133px;
    }

    .newfound .info-normal .text {
        float: left;
        margin: 16px 10px;
        height: 40px;
        overflow: hidden;

        display: -webkit-box;  /*将对象作为弹性盒子模型显示*/
        text-overflow:ellipsis;
        word-break:break-all;
        -webkit-box-orient:vertical;/*伸缩盒对象的子元素的排列方式-垂直*/
        -webkit-line-clamp:2; /*限制在一个块级元素显示的文本的行数*/
    }

    .textinfolist {
        width: 378px;
    }
    .media.textinfolist{
        width: 582px;
        float: left;
        margin-right: 35px;
    }

    .mediacoverage .media.textinfolist li{
        height: auto;
        padding: 0;
        padding-top: 15px;
        padding-bottom: 5px;
    }
    .mediacoverage .media-wrap{
        margin-right: -35px;margin-top: -15px
    }
    .mediacoverage .media.textinfolist li .title{
        height: auto;
        margin-bottom: 0;
        font-size: 15px;
    }
    .mediacoverage .media.textinfolist li > a p{
        width: 490px;
        overflow: hidden;white-space: nowrap;text-overflow: ellipsis;
    }
    .mediacoverage .media.textinfolist .time{
        line-height: 22px;
    }

    .textinfolist li {
        max-height: 86px;
        overflow: hidden;
        border-bottom: 2px solid #979797;
        padding: 8px 0;
    }

    .textinfolist li>a{width: 100%;}
    
    .textinfolist .title {
        font-size: 18px;
        color: #000;
        position: relative;
        margin-bottom: 5px;
    }

    .newfound .textinfolist .title {
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
    }

    .textinfolist .title .point {
        display: block;
        width: 5px;
        height: 5px;
        background: #000;
        border-radius: 50%;
        position: absolute;
        left: 0;
        top: 10px;
    }
    .newfound .textinfolist .title>p{
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
    }
    .newfound .textinfolist li a>p{
        display: -webkit-box;  /*将对象作为弹性盒子模型显示*/
        text-overflow:ellipsis;
        word-break:break-all;
        -webkit-box-orient:vertical;/*伸缩盒对象的子元素的排列方式-垂直*/
        -webkit-line-clamp:3; /*限制在一个块级元素显示的文本的行数*/
    }
    .textinfolist li p {
        max-height: 58px;
        overflow: hidden;
        padding-left: 15px;
        line-height: 1.4;
    }


        /*精选案例*/
    .caseselected .cont > li {
        float: left;
        width: 392px;
        height: 420px;
        background: #fff;
        margin-right: 10px;
        margin-bottom: 10px;
        position: relative;
    }

    .caseselected li:nth-child(3n) {
        margin-right: 0;
    }

    .caseselected .img {
        width: 100%;
        height: 264px;
        background: #ddd;
        overflow: hidden;
    }

    .caseselected .title {
        color: #000;
        font-size: 18px;
        padding-bottom: 5px;
        height: 58px;
        overflow: hidden;
        box-sizing: border-box;

        display: -webkit-box;  /*将对象作为弹性盒子模型显示*/
        text-overflow:ellipsis;
        word-break:break-all;
        -webkit-box-orient:vertical;/*伸缩盒对象的子元素的排列方式-垂直*/
        -webkit-line-clamp:2; /*限制在一个块级元素显示的文本的行数*/
    }

    .caseselected .textinfo {
        padding: 8px 10px 12px;
    }

    .caseselected .tags span {
        display: inline-block;
        height: 28px;
        line-height: 28px;
        padding: 0 20px;
        background: #fff;
        border: 1px solid #000;
        color: #666;
        margin-right: 5px;
        margin-top: 5px;
    }

    .caseselected .numbs {
        position: absolute;
        right: 15px;
        bottom: 15px;
        color: #666;
    }

    .caseselected .numbs li {
        position: relative;
        height: 25px;
        line-height: 25px;
        padding-left: 32px;
        margin-left: 30px;
    }

    .caseselected .numbs i {
        display: inline-block;
        position: absolute;
        left: 0;
        top: 0;
    }

    i.scan {
        background: url("/static/images/home/icon-scan.png") no-repeat center;
    }

    i.zan {
        background: url("/static/images/home/icon-zan.png") no-repeat center;
    }

    /*媒体报道*/
    .mediacoverage .textinfolist li {
        height: 70px;
        padding-top: 7px;
        overflow: hidden;
    }

    .mediacoverage .textinfolist li > a {
        width: 100%;
    }

    .mediacoverage .textinfolist li > a p{
        color: #000;
    }

    .mediacoverage .textinfolist .title {
        height: 48px;
        overflow: hidden;
    }

    .mediacoverage .textinfolist .time {
        text-align: right;
    }

    .imglogo-media {
        width: 795px;
        height: 320px;
        padding: 15px 0;
        overflow: hidden;
        background: #fff;
    }

    /*合作品牌*/
    .logofriends .cont {
        width: 1200px;
        height: 157px;
        background: #fff;
    }

    /*swiper*/
    .citySelection .btns{
        z-index: 99;
    }
</style>




