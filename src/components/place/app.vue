<template>
    <div>
        <!--<div class="w1200 topback">-->
            <!--<a class="back" href="javascript:;"><i class="icon-arrowleft"></i> 返回搜索</a>-->
        <!--</div>-->

        <div class="w1200 events-dtlbox clearfix">
        <div class="spacedtl clearfix">
            <div class="fl logo"><img :src="placeDtl.logo" onerror="javascript:this.src='/static/images/avatar.png';" width="100%" height="100%"></div>
            <div class="fl evdtlcont">
                <div class="title">
                    <h2>{{placeDtl.title}}</h2>
                    <div class="icons-text">
                        <i class="icons icon-place"></i>
                        <p class="title">区域位置：{{placeDtl.city_name}} | {{placeDtl.district}} | {{placeDtl.address}}</p>
                    </div>
                    <a @click="changeCollect" href="javascript:;" class="collect">
                        <i class="icons" :class="[ placeDtl.follow == true ? 'icon-collect-hv' : 'icon-collect']"></i>
                        <span>收藏</span>
                    </a>
                </div>
                <div class="intro">
                    <h5>场地介绍</h5>
                    <p>{{placeDtl.brand_story}}</p>
                </div>
                <div class="reason">
                    <h6>推荐理由</h6>
                    <div class="icons-text">
                        <i class="icons icon-zan-red"></i>
                        <p class="title">{{placeDtl.recommend_reason}}</p>
                    </div>
                </div>
            </div><!--evdtlcont-end-->
            <div class="fr evdtllist">
                <div class="title">
                    <i class="icons icon-space"></i>
                    <p>拥有<span class="red">{{placeDtl.count_space}}</span>个空间</p>
                </div>
                <div class="cont">
                    <dl>
                        <i class="icons icon-pnumbs"></i>
                        <dt>最大容纳</dt>
                        <dd>{{placeDtl.max_people}}人</dd>
                    </dl>
                    <dl>
                        <i class="icons icon-assort"></i>
                        <dt>场地配套</dt>
                        <dd>
                            {{placeDtl.facilities}}
                            <!--<span>洗手间</span>｜-->
                            <!--<span>化妆间</span>｜-->
                            <!--<span>空调暖气</span>｜-->
                            <!--<span>网络WIFI</span> ｜-->
                            <!--<span>货运电梯</span>｜-->
                            <!--<span>灯光音响</span>｜-->
                            <!--<span>投影LED</span>-->
                        </dd>
                    </dl>
                    <dl>
                        <i class="icons icon-busintype"></i>
                        <dt>行业类型</dt>
                        <dd>
                            <!--<span>通用</span> ｜-->
                            <!--<span>IT类</span>｜-->
                            <!--<span>公益事业</span>｜-->
                            <!--<span>教育</span>｜-->
                            <!--<span>通讯</span>-->
                            {{placeDtl.industry_field}}
                        </dd>
                    </dl>
                    <dl>
                        <i class="icons icon-evtype"></i>
                        <dt>活动类型</dt>
                        <dd>
                            <!--<span>文体娱乐</span>｜-->
                            <!--<span>会议会务</span>｜-->
                            <!--<span>培训演讲</span>-->
                            {{placeDtl.service_type}}
                        </dd>
                    </dl>
                </div>
            </div><!--evdtllist-end-->
        </div>
        <!--spacedtl-end-->

        <!--内容部分-->
        <div class="spacecont clearfix">
            <div class="fl left">
                <div class="spacetitle">场地空间</div>
                <ul class="recommend clearfix">
                    <li v-for="item in spaces">
                        <div class="img">
                            <router-link :to="'/space/'+item.id">
                                <img :src="item.img_paths.length > 0 ? item.img_paths[0]['url_400_267'] : ''">
                            </router-link>
                        </div>
                        <div class="text">
                            <router-link class="title" :to="'/space/'+item.id">
                                {{item.name}}
                            </router-link>
                            <!--<a class="title" href="javascript:;">{{item.name}}</a>-->
                            <div class="textinfo">
                                <p>最大容纳：{{item.Max_seating_capacity}}人</p>
                                <p>落位区域：{{item.through_three_areas}}</p>
                                <p>空间面积：{{item.area}}㎡</p>
                            </div>
                        </div>
                    </li>
                </ul>
            </div>

            <div class="fr right">
                <!--相关专题-->
                <div class="rtsubject">
                    <div class="spacetitle">相关专题</div>
                    <ul class="rtspacelist">
                        <li class="clearfix" v-for="item in relate_topics">
                            <router-link class="fl img" :to="item.special_url ? item.special_url : '/article/' + item.id">
                                <img :src="item.img_paths.length > 0 ? item.img_paths[0]['url_150_100'] : ''">
                            </router-link>
                            <!--<a class="fl img" href="javascript:;">-->
                                <!--<img src="">-->
                            <!--</a>-->
                            <router-link class="fr text" :to="item.special_url ? item.special_url : '/article/' + item.id">
                                {{item.title}}
                            </router-link>
                            <!--<a class="fr text" href="javascript:;">-->
                                <!--{{item.title}}-->
                            <!--</a>-->
                        </li>
                        <!--<li class="clearfix">-->
                            <!--<a class="fl img" href="javascript:;">-->
                                <!--<img src="">-->
                            <!--</a>-->
                            <!--<a class="fr text" href="javascript:;">-->
                                <!--魔都最具创意的十大会务中心，不仅仅只是为了开会-->
                            <!--</a>-->
                        <!--</li>-->
                    </ul>
                </div>

                <!--相关资讯-->
                <div class="rtinformation">
                    <div class="spacetitle">相关资讯</div>
                    <ul class="rtspacelist">
                        <li class="clearfix" v-for="item in relate_articles">
                            <router-link class="fl img" :to="'/article/'+item.id">
                                <img :src="item.img_paths.length > 0 ? item.img_paths[0]['url_150_100'] : ''">
                            </router-link>
                            <!--<a class="fl img" href="javascript:;">-->
                            <!--<img src="">-->
                            <!--</a>-->
                            <router-link class="fr text" :to="'/article/'+item.id">
                                {{item.title}}
                            </router-link>
                            <!--<a class="fr text" href="javascript:;">-->
                            <!--{{item.title}}-->
                            <!--</a>-->
                        </li>
                        <!--<li class="clearfix">-->
                            <!--<a class="fl img" href="javascript:;">-->
                                <!--<img src="">-->
                            <!--</a>-->
                            <!--<a class="fr text" href="javascript:;">-->
                                <!--魔都最具创意的十大会务中心，不仅仅只是为了开会-->
                            <!--</a>-->
                        <!--</li>-->
                    </ul>
                </div>

            </div><!--right-end-->
        </div><!--spacecont-end-->
    </div><!--events-dtlbox-end-->
    </div>

</template>

<script>
    import Lib from 'assets/Lib.js';
    //import Jquery from 'assets/jquery-3.1.0.min.js'

    import 'assets/css/component.css';
    import 'assets/css/hold-event.css';

    import moduleHeader from 'components/module-header';
    import moduleFooter from 'components/module-footer';

    export default {
        data() {
            return {
                phone:'',
                password:'',
                username:'',
                spacesubs:[
                        1,2,3
                ],
                placeDtl : [],
                spaces : [],
                relate_topics : '',
                relate_articles : '',
                changeCollectPromise : ''
            }
        },
        mounted () {
            var self = this;

            self.$store.commit('loading',true); //显示loading 状态
            $.get({
                url: window.YUNAPI.placeDtl + '/' + this.$route.params.id,
                data: self.$store.getters.validationData,
                success: function (data) {
                    self.placeDtl = data.site
                    self.$parent.loading = false;
                    self.spaces = data.site_spaces
                    self.relate_topics = data.relate_topics
                    self.relate_articles = data.relate_articles
                    self.$store.commit('loading',false); //显示loading 状态
                },
                error: function () {
                    GlobleFun.httpError()
                }
            });
        },
        computed : {
            personalData (){
                return this.$store.state.personalData
            }
        },
        methods: {
            changeCollect(){
                var self = this;
                if( this.changeCollectPromise && this.changeCollectPromise.state() == 'pending'){
                    return
                }
                if(!self.personalData.id){
                    APP.$message({
                        message: '请先登录!',
                        type: 'warning'
                    });
                    return
                }
                self.changeCollectPromise = $.post({
                    url: window.YUNAPI.changeCollect,
//                    data : {
//                        user_id : self.personalData.id,
//                        followable_type : 'Site',
//                        followable_id : self.placeDtl.id
//                    },
                    data : GlobleFun.objConcat(self.$store.getters.validationData,{
                        user_id : self.personalData.id,
                        followable_type : 'Site',
                        followable_id : self.placeDtl.id
                    }),
                    success: function (data) {

                        if(data.status == 1){
                            self.placeDtl.follow = !self.placeDtl.follow
                        }
                        GlobleFun.httpMessage(data)
                    },
                    error : function () {

                    }
                });
            }
        },

        //记住密码
        rememberPassword(){}
    }

</script>






