<template>

    <div class="w1200 ip-page">
        <div class="top-banner">
            <img src="/static/images/ip/banner.jpg" alt="">
        </div>
        <div class="module-header">
            <span>品牌推荐</span>
        </div>
        <div class="yun-swiper-wrap2 brand-swiper">
            <div class="swiper-container relative-topic-swiper">
                <div class="swiper-wrapper">
                    <div class="swiper-slide topic-pic" v-for="item in ipRecommend">
                        <img :src="item.img_paths.length > 0 ? item.img_paths[0]['url_590_400'] : ''" alt="">
                    </div>
                </div>
                <!-- Add Pagination -->
                <!--<div class="swiper-pagination"></div>-->
                <!-- Add Arrows -->
                <div class="yun-swiper-prev">
                    <span class="icon-arrowleft black"></span>
                </div>
                <div class="yun-swiper-next ">
                    <span class="icon-arrowright black"></span>
                </div>
            </div>
        </div>
        <div class="module-header">
            <span>IP类别</span>
        </div>
        <div class="ip-category clearfix">
            <router-link to="/iplist">全部</router-link>
            <router-link :to="'/iplist?p_type='+key" v-for="(key,value,index) in ipType" v-if="index < 7">{{value}}</router-link>
            <!--<a href="" v-for="(key,value,index) in ipType" v-if="index < 7">{{value}}</a>-->
            <router-link to="/iplist">更多</router-link>
            <!--<a href="">更多</a>-->
            <!--<a href="">动漫</a>-->
            <!--<a href="">卡通</a>-->
            <!--<a href="">影视</a>-->
            <!--<a href="">游戏</a>-->
            <!--<a href="">市集</a>-->
            <!--<a href="">市集</a>-->
            <!--<a href="">市集</a>-->
            <!--<a href="">市集</a>-->
        </div>
        <div class="module-header">
            <span>精选推荐</span>
            <!--<a href="" class="more">-->
                <!--查看更多-->
                <!--<i class="icon icon-arrowright"></i>-->
            <!--</a>-->
            <router-link to="/iplist" class="more">
                查看更多
                <i class="icon icon-arrowright"></i>
            </router-link>
        </div>
        <div class="concentration clearfix">
            <ul>
                <li v-for="item in ipProject">
                    <a href="javascript:;"><img :src="item.img_paths.length > 0 ? item.img_paths[0]['url_590_400'] : ''" alt=""></a>
                    <div class="rec-dtl">
                        <!--<button class="op-coop" @click.native="dialogVisible = true">合作咨询</button>-->
                        <el-button class="op-coop" type="text" @click  @click.native="consultClick(item.id,item.title)">合作咨询</el-button>
                        <!--<el-button type="text" >点击打开 Dialog</el-button>-->
                        <p class="title">{{item.title}}</p>
                        <p class="tag">{{item.keyword}}</p>
                        <div class="dl-wrap clearfix">
                            <dl><dt>类别 : </dt><dd>{{item.p_type}}</dd></dl>
                            <dl><dt>来源 :</dt><dd>{{item.source}}</dd></dl>
                            <dl><dt>场地面积 :</dt><dd>{{item.area}}㎡</dd></dl>
                        </div>
                        <div class="">
                            <dl><dt>适用人群 :</dt><dd>{{item.applicable_people}}</dd></dl>
                            <dl><dt>预算范围 :</dt><dd>{{item.budget_amount}}</dd></dl>
                        </div>
                        <p class="des">{{item.p_notes}}</p>
                    </div>
                </li>
            </ul>
        </div>
        <div class="module-header">
            <span>精选案例</span>
            <!--<a href="" class="more">-->
                <!--查看更多-->
                <!--<i class="icon icon-arrowright"></i>-->
            <!--</a>-->
            <router-link class="more" to="/found?caseType=6&selectType=caseType&selectTypeKey=6">
                查看更多
                <i class="icon icon-arrowright"></i>
            </router-link>
        </div>
        <div class="case-list">
            <ul class="clearfix">
                <li v-for="item in ipCase">
                    <router-link :to="'/article/'+item.id">
                        <img :src="item.first_picture.url" alt="">
                        <p class="case-des">{{item.title}}</p>
                    </router-link>
                    <!--<a href="">-->
                        <!---->
                    <!--</a>-->
                </li>
            </ul>
        </div>
        <div class="module-header">
            <span>平台优势</span>
        </div>
        <div class="platform-super">
            <ul class="clearfix">
                <li>
                    <span class="super-icon"><img src="/static/images/ip/pt1.png" alt=""></span>
                    <p>全面整合文创资源</p>
                    <p>（已有合作版权近50家）</p>
                </li>
                <li>
                    <span class="super-icon"><img src="/static/images/ip/pt2.png" alt=""></span>
                    <p>一站式采购</p>
                    <p>省心又省力</p>
                </li>
                <li>
                    <span class="super-icon"><img src="/static/images/ip/pt3.png" alt=""></span>
                    <p>全方位合作模式</p>
                    <p>高人气&高收益</p>
                </li>
                <li>
                    <span class="super-icon"><img src="/static/images/ip/pt4.png" alt=""></span>
                    <p>极大减少版权费</p>
                    <p>有效降低运营成本</p>
                </li>
                <li>
                    <span class="super-icon"><img src="/static/images/ip/pt5.png" alt=""></span>
                    <p>全国性平台</p>
                    <p>多城市全面推广</p>
                </li>
            </ul>
        </div>
        <div class="module-header">
            <span>团队优势</span>
        </div>
        <div class="team-super">
            <ul class="clearfix">
                <li>
                    <span class="super-icon"><img src="/static/images/ip/td1.png" alt=""></span>
                    <p>10 年商业地产运营经验</p>
                </li>
                <li>
                    <span class="super-icon"><img src="/static/images/ip/td2.png" alt=""></span>
                    <p>7 年创意领域实际操作经验</p>
                </li>
                <li>
                    <span class="super-icon"><img src="/static/images/ip/td3.png" alt=""></span>
                    <p>丰富的广告创意&活动执行经验</p>
                </li>
            </ul>
        </div>
        <consult-form ref="consult"></consult-form>
    </div>

</template>

<script>

    import Lib from 'assets/Lib.js';
    import 'assets/css/hold-event.css';
    require ('assets/css/component.css')
    require ('assets/css/ip.css')
    import 'assets/libs/swiper/swiper.js'
    import 'assets/Libs/jquery.validate.js';
    import consultForm from './consultForm.vue';

    export default {
        data(){
            return {

                ipCase : [],
                ipRecommend : [],
                ipProject : [],
                ipType : [],
                ipTypeValues : [],
                cdVisible : true,
                username : '',
                comment :'',
                consult : {
                    username : '',
                    phone : '',
                    content : '',
                    project_id : '',
                    consultCity : '上海'
                }
            }

        },
        mounted () {
            var self = this;
            self.$store.commit('loading',true);
            $.ajax({

                url: window.YUNAPI.findIp,
                data : {
                    city_id : self.$store.state.city_id
                },
                success: function (data) {

                    self.$store.commit('loading',false);

                    self.ipCase = data.ip_case
                    self.ipProject = data.ip_project
                    self.ipRecommend = data.ip_recommend;
                    // 关键词 需要按,分割
                    for (var i = 0; i < self.ipProject.length - 1; i++){
                        self.ipProject[i].keyword = self.ipProject[i].keyword.replace(',',' ');
                    }

                    self.ipType = data.ip_type


//                    for (var i in data.ip_type){
//                        var k = {
//                            ke : i,
//                            v : data.ip_type[i]
//                        }
//
//                        self.ipType.push(k)
//                    }
                    setTimeout(function () {
                        self.init();
                    },300)
                },
                error : function () {

                }
            });

            $(function() {

                $("#login").validate();

                $.validator.methods.equal = function(value, element, param) {
                    return value == param;
                };
                $("#submit-consult").validate({
                    debug: true,
                    errorElement: "div",
//                    errorClass : 'warning',
                    errorPlacement: function(error, element) {
                        error.addClass('warning').appendTo(element.parent("li"));
                        error.parent('li').addClass('war')
                    },
                    success : function (e) {
                        e.parents('li').removeClass('war');
                        e.parents('li').find('.warning').remove();
                    },
                    rules : {
                        phone : {
                            required : true,
//                            minlength : 11,
                            // 自定义方法：校验手机号在数据库中是否存在
                            // checkPhoneExist : true,
                            isMobile : true
                        },
                    }
                })
            })
        },
        components: {
            consultForm
        },

        methods: {
            init : function () {
                var swiper2 = new Swiper('.relative-topic-swiper', {
                    pagination: '.swiper-pagination',
                    nextButton: '.yun-swiper-next',
                    prevButton: '.yun-swiper-prev',
                    slidesPerView: 3,
                    centeredSlides: false,
                    spaceBetween: 10,
                    paginationHide:true,
                    autoplay: 3000
                });
            },
//            submitConsult : function () {
//                var self = this;
//                //console.log(self.consult);
//                $.post({
//                    url: window.YUNAPI.submitConsult,
//                    data : self.consult,
//                    success: function (data) {
//                        console.log(data);
//                        self.$message({
//                            message: '恭喜你，这是一条成功消息',
//                            type: 'success'
//                        });
//                    },
//                    error : function () {
//
//                    }
//                });
//            },
            consultClick : function (id,title) {
                this.$refs.consult.consult.title = title;
                this.$refs.consult.consult.project_id = id;
                this.$refs.consult.cdVisible = true;
            }
        }
    }
</script>





