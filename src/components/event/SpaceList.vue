<template>
    <div class="w1200 mt20 pagination-fore-end">
        <div class="condition-wrap clearfix">
            <!--<div class="condition-sp">-->
                <!--<span class="icon-text">区域范围</span>-->
                <!--<el-select v-model="valType" class="select-text">-->
                    <!--<el-option-->
                            <!--v-for="item in areaRange"-->
                            <!--:label="item.label"-->
                            <!--:value="item.value">-->
                    <!--</el-option>-->
                <!--</el-select>-->
            <!--</div>-->
            <!--<div class="condition-sp">-->
                <!--<span class="icon-text">行政区域</span>-->
                <!--<p class="select-text">全部</p>-->
                <!--<div class="sub-condition clearfix">-->
                    <!--&lt;!&ndash;<ul class="condition-left">&ndash;&gt;-->
                        <!--&lt;!&ndash;<li>全部</li>&ndash;&gt;-->
                        <!--&lt;!&ndash;<li>全部</li>&ndash;&gt;-->
                        <!--&lt;!&ndash;<li>全部</li>&ndash;&gt;-->
                        <!--&lt;!&ndash;<li>黄埔区</li>&ndash;&gt;-->
                    <!--&lt;!&ndash;</ul>&ndash;&gt;-->
                    <!--&lt;!&ndash;<ul class="condition-right">&ndash;&gt;-->
                        <!--&lt;!&ndash;<li>&ndash;&gt;-->
                            <!--&lt;!&ndash;<el-checkbox class="checkbox" checked>备选项</el-checkbox>&ndash;&gt;-->
                        <!--&lt;!&ndash;</li>&ndash;&gt;-->
                        <!--&lt;!&ndash;<li>&ndash;&gt;-->
                            <!--&lt;!&ndash;<el-checkbox class="checkbox" checked>备选项</el-checkbox>&ndash;&gt;-->
                        <!--&lt;!&ndash;</li>&ndash;&gt;-->
                        <!--&lt;!&ndash;<li>&ndash;&gt;-->
                            <!--&lt;!&ndash;<el-checkbox class="checkbox" checked>备选项</el-checkbox>&ndash;&gt;-->
                        <!--&lt;!&ndash;</li>&ndash;&gt;-->
                        <!--&lt;!&ndash;<li>&ndash;&gt;-->
                            <!--&lt;!&ndash;<el-checkbox class="checkbox" checked>备选项</el-checkbox>&ndash;&gt;-->
                        <!--&lt;!&ndash;</li>&ndash;&gt;-->
                        <!--&lt;!&ndash;<li>&ndash;&gt;-->
                            <!--&lt;!&ndash;<el-checkbox class="checkbox" v-model="checked" checked>备选项</el-checkbox>&ndash;&gt;-->
                        <!--&lt;!&ndash;</li>&ndash;&gt;-->
                    <!--&lt;!&ndash;</ul>&ndash;&gt;-->
                <!--</div>-->
            <!--</div>-->
            <div class="condition-sp">
                <span class="icon-text">场地类型</span>
                <el-select v-model="searchData.space_type" class="select-text" @change="selectSearch">
                    <el-option
                            v-for="(value,key) in searchCondition.space_type"
                            :label="key"
                            :value="value">
                    </el-option>
                </el-select>
            </div>
            <div class="condition-sp">
                <span class="icon-text">价格</span>
                <el-select v-model="searchData.budget_amount" class="select-text" @change="selectSearch">
                    <el-option
                            v-for="(value,key) in searchCondition.budget_amount"
                            :label="value"
                            :value="key">
                    </el-option>
                </el-select>
            </div>
            <div class="condition-sp">
                <span class="icon-text">可用面积</span>
                <el-select v-model="searchData.area_size" class="select-text" @change="selectSearch">
                    <el-option
                            v-for="(value,key) in searchCondition.area_size"
                            :label="value"
                            :value="key">
                    </el-option>
                </el-select>
            </div>
        </div>
        <div class="search-content spacelists">
            <div class="w1200 mt20 clearfix">
                <div class="space-list">
                    <div class="search-input-wrap clearfix">

                        <div class="inputbox clearfix">
                            <div class="fl citySelect spacelistInput" style="width: 120px">
                                <div class="result">
                                    <el-select v-model="spaceSearchCondition.city_id" @change="search">
                                        <el-option
                                                v-for="item in searchCondition.cities"
                                                :label="item.name"
                                                :value="item.id">
                                        </el-option>
                                    </el-select>
                                </div>
                            </div>

                            <input @keyup.enter="spaceSearch" class="" type="text" placeholder="商圈／地标／机场／火车站／场地名" v-model='spaceSearchCondition.q.keyword'>
                            <button class="searchbtn" @click="spaceSearch">搜索</button>
                        </div>
                    </div>
                    <div class="list">
                        <ul class="recommend recommend-sub list-piece clearfix">
                            <li v-for="spacesub in spacesubs">
                                <div class="img">
                                    <a :href="'/space/'+spacesub.id" target="_blank">
                                        <img onerror="javascript:this.src='/static/images/error.jpg';" :src="spacesub.img_paths.length > 0 ? spacesub.img_paths[0]['url_400_267'] : ''">
                                    </a>
                                </div>
                                <div class="text">
                                    <a target="_blank" class="title" :href="'/space/'+spacesub.id">{{spacesub.name}}</a>
                                    <div class="price">{{spacesub.special_price}}</div>
                                    <div class="textinfo">
                                        <p><span>场地类型：</span>{{spacesub.site_type}}</p>
                                        <p><span>落位区域：</span>{{spacesub.through_three_areas}}</p>
                                        <p><span>容纳人数：</span>{{spacesub.site_max_people}}人</p>
                                        <div class="numb clearfix">
                                            <p><span>面积：</span>{{spacesub.area}}㎡</p>
                                            <p><span>层高：</span>{{spacesub.height}}m</p>
                                        </div>
                                        <p><span>地址：</span>{{spacesub.city_name}}&nbsp;{{spacesub.areas}}&nbsp;{{spacesub.address}}</p>
                                    </div>

                                    <a @click="addInquiry(spacesub.id,spacesub.name)" class="btnjoin"
                                       v-bind:class=" {'hv' : inquiryList.hasOwnProperty(spacesub.id)}" href="javascript:;"
                                        v-text="inquiryList.hasOwnProperty(spacesub.id) ? '已加入询价' : '加入询价' ">
                                    </a>
                                    <!--<a class="btnjoin hv" href="javascript:;">已加入询价单</a>-->
                                </div>
                            </li>
                        </ul>

                        <!--无结果-->
                        <div class="noresult" v-if="spacesubs.length <= 0">
                            <h2>抱歉，暂时没有符合的结果</h2>
                            <p>将你的活动需求提交给云SPACE<br>
                                30分钟内场地顾问为您提供免费的场地匹配服务
                            </p>

                            <div class="form-holdenent">
                                <div class="title">我要办活动</div>
                                <ul class="inputbox">
                                    <li class="selectwrap">
                                        <!--活动人数-->
                                        <el-select v-model="demand.number_of_activities" placeholder="您的活动人数?">
                                            <el-option
                                                    v-for="(value,key) in searchCondition.activity_people"
                                                    :label="value"
                                                    :value="key">
                                            </el-option>
                                        </el-select>
                                    </li>
                                    <li class="selectwrap">
                                        <!--活动类型-->
                                        <el-select v-model="demand.activity_type" placeholder="您的活动类型?">
                                            <el-option
                                                    v-for="(v,k) in searchCondition.activity_type"
                                                    :label="v"
                                                    :value="k">
                                            </el-option>
                                        </el-select>
                                    </li>
                                    <li class="text">省时，省心，找你所想...</li>
                                    <li>
                                        <button class="holdeventbtn" @click="gotoHoldEvent">下一步</button>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>
                    <el-pagination
                            @sizechange="handleSizeChange"
                            @current-change="handleCurrentChange"
                            :current-page="page"
                            :page-size="12"
                            layout="prev, pager, next, jumper"
                            v-if="spacesubs.length > 0"
                            :total="total">
                    </el-pagination>

                </div>
                <div class="search-left">
                    <div class="tags clearfix">
                        <a v-for="item in tags" href="javascript:;" @click="keywordClick(item)">{{item}}</a>
                    </div>
                    <!--<div class="search-left-map"></div>-->
                    <div class="enquiry-tip" v-if="inquiryCount <= 0">
                        您还没有添加任何空间!
                    </div>
                    <!--<button class="key-enquiry-btn">-->
                        <!--一键询价-->
                        <!--<span class="enquiry-num">{{inquiryCount}}</span>-->

                    <!--</button>-->
                    <router-link class="key-enquiry-btn" to="/inquiry">
                        一键询价
                        <span class="enquiry-num">{{inquiryCount}}</span>
                    </router-link>
                </div>
            </div>

        </div>
    </div>
</template>

<script>

    import Lib from 'assets/Lib.js'

    import 'assets/css/component.css';
    import 'assets/css/hold-event.css';
    export default {
        data() {
            return {
                checked: true,
                areaRange: [ ],
                spacemains: [
                    1, 2, 3, 4, 5, 6
                ],
                tags :[],
                spacesubs: [ ],
                valType:'选项一',
                page: 1,
                total: 0,
                demand : {
                    phone : '',
                    contact : '',
                    order_city : 1,
//                    number_of_activities : "50",
                    number_of_activities : null,
                    time : ['',''],
                    user_id : 1,
                    activity_type : '',
//                    activity_type : '零售短租',
                    auth_code : '',
                    activities_required : '',
                    code_token : '',
                    s_time:'',
                    e_time:'',
                    ip_city:'上海'
                },
                searchData : {
                    space_type : '',
                    area_size : '',
                    budget_amount : ''

                },
                selectSearchReady : false
            }
        },

        computed : {
            searchCondition (){
                var s = this.$store.state.searchCondition
                var self = this
                if(s.space_type){
                    s.space_type['不限'] = ''
                    setTimeout(function () {
                        self.selectSearchReady = true
                    },300)
                }
                return s
            },
            spaceSearchCondition () {
                var s = this.$store.state.spaceSearchCondition
                var self = this
                if(s.q.site_site_type_eq){
                    self.searchData.space_type = s.q.site_site_type_eq + ''
                }
                if(typeof this.$route.query.type != 'undefined' && this.$route.query.type == 'all'){
                    s.q.site_site_type_eq = ''
                    self.searchData.space_type = s.q.site_site_type_eq + ''
                }
                if(!s.city_id){ // 如果城市不存在  设置默认城市 为头部选择的城市
                    s.city_id = self.$store.state.city_id

                }

                return s
            },
            inquiryCount () {
                return this.$store.state.inquiryCount
            },
            inquiryList () {
                return this.$store.state.inquiryList
            }
        },
        mounted () {
            var self = this;
            if(typeof this.$route.query.q != 'undefined'){
                this.spaceSearchCondition.q.keyword = this.$route.query.q
                self.spaceSearchCondition.city_id = self.$store.state.city_id
            }

            if(typeof this.$route.query.site_site_type_eq != 'undefined'){
                this.spaceSearchCondition.q.site_site_type_eq = this.$route.query.site_site_type_eq
            }

            self.search();

        },
        components: {},
        methods: {
            search : function () {
                var self = this;
                self.$store.commit('loading',true);
                self.spaceSearchCondition.page = this.page
                this.spaceSearchCondition.q.site_site_type_eq = this.searchData.space_type
                //搜索 价格现在
                if(self.searchData.budget_amount){
                    var budget_amount = self.searchData.budget_amount.split('-')
                    self.spaceSearchCondition.q.market_price_gteq = budget_amount[0]
                    self.spaceSearchCondition.q.market_price_lteq = budget_amount[1]
                }else{
                    self.spaceSearchCondition.q.market_price_gteq = ''
                    self.spaceSearchCondition.q.market_price_lteq = ''
                }

                //搜索 面积限制
                if(self.searchData.area_size){
                    var area_size = self.searchData.area_size.split('-')
                    self.spaceSearchCondition.q.area_gteq = area_size[0]
                    self.spaceSearchCondition.q.area_lteq = area_size[1]
                }else{
                    self.spaceSearchCondition.q.area_gteq = ''
                    self.spaceSearchCondition.q.area_lteq = ''
                }

                $.ajax({
                    url: window.YUNAPI.SpaceList,
                    data : self.spaceSearchCondition,
                    success:function (data) {
                        self.spacesubs=data.spaces;
                        self.total = data.page_count
                        //场地类型
                        for(var i = 0; i < self.spacesubs.length - 1; i++){
                            self.spacesubs[i].keyword = self.spacesubs[i].keyword.replace(',','|');
                        }

                        //标签推荐
                        self.tags=data.space_keywords;
                        self.$store.commit('loading',false);
                    }
                });
            },
            selectSearch(){
                if(this.selectSearchReady){
                    this.search()
                }
            },
            handleSizeChange(val) {
            },
            handleCurrentChange(val) {
                this.page = val
                this.search()
            },
            spaceSearch : function () {
                this.$store.commit('spaceSearchCondition', this.spaceSearchCondition);
                this.search();
            },
            addInquiry : function (id,name) {
//                LS.set('inquiry',[id,name])
                this.$store.commit('inquiryChange',{id : id, name : name, type : 2});
            },
            gotoHoldEvent : function () {
//                router.push('/event/hold')
                router.push({ path: '/event/hold', query: { activity_type: this.demand.activity_type, number_of_activities : this.demand.number_of_activities}})
            },
            keywordClick(keyword){
                this.spaceSearchCondition.q.keyword = keyword
                this.search();
            }
        }
    }
</script>

<style scoped>

</style>





