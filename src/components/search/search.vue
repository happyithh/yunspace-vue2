<template>
    <div class="pagination-fore-end search-h">
        <div class="wrap100">
            <div class="w1200 condition-wrap clearfix screening-wrap">
                <div class="condition-sp">
                    <span class="icon-title"><i class="s-icon icon-citys"></i>城市</span>
                    <el-select v-model="urlData.city_id" class="select-text">
                        <el-option
                                v-for="item in searchCondition.cities"
                                :label="item.name"
                                :value="item.id">
                        </el-option>
                    </el-select>
                </div>

                <!--场地类型-->
                <div class="condition-sp">
                    <span class="icon-title"><i class="s-icon icon-place"></i>场地类型</span>
                    <el-select v-model="urlData.q.site_type_eq" class="select-text">
                        <el-option
                                v-for="(value,key) in searchCondition.space_type"
                                :label="key"
                                :value="value">
                        </el-option>
                    </el-select>
                </div>

                <!--活动类型-->
                <!--<div class="condition-sp">-->
                    <!--<span class="icon-title"><i class="s-icon icon-active"></i>活动类型</span>-->
                    <!--<el-select v-model="urlData.business_circle" class="select-text">-->
                        <!--<el-option-->
                                <!--v-for="(value,key) in searchCondition.activity_type"-->
                                <!--:label="key"-->
                                <!--:value="value">-->
                        <!--</el-option>-->
                    <!--</el-select>-->
                <!--</div>-->

                <!--容纳人数-->
                <div class="condition-sp">
                    <span class="icon-title"><i class="s-icon icon-people"></i>容纳人数</span>
                    <el-select v-model="searchData.search_people" class="select-text">
                        <el-option
                                v-for="(value,key) in searchCondition.search_people"
                                :label="value"
                                :value="key">
                        </el-option>
                    </el-select>
                </div>

                <!--预算范围-->
                <div class="condition-sp">
                    <span class="icon-title"><i class="s-icon icon-budget"></i>预算范围</span>
                    <el-select v-model="searchData.budget_amount" class="select-text">
                        <el-option
                                v-for="(value,key) in searchCondition.budget_amount"
                                :label="value"
                                :value="key">
                        </el-option>
                    </el-select>
                </div>

                <!--面积范围-->
                <!--<div class="condition-sp">-->
                    <!--<span class="icon-title"><i class="s-icon icon-size"></i>面积范围</span>-->
                    <!--<el-select v-model="searchData.area_size" class="select-text">-->
                        <!--<el-option-->
                                <!--v-for="(value,key) in searchCondition.area_size"-->
                                <!--:label="value"-->
                                <!--:value="key">-->
                        <!--</el-option>-->
                    <!--</el-select>-->
                <!--</div>-->

                <!--搜索、提交按钮-->
                <div class="fr screen-btn clearfix">
                    <button class="fl btn" @click="getData">搜索</button>
                    <!--<a href="/search/dtl" class="fr btn">提交<span class="num">3</span></a>-->
                    <el-button class="fr btn" type="text" @click="spaceSubmit">提交<span class="num">{{spaceManageSelectCount}}</span></el-button>
                </div>
            </div>
        </div>
        <div class="w1200 mt20 search-content spacelists">
            <div class="w1200 mt20 clearfix">
                <div class="side-screening fl">
                    <!--场地位置-->
                    <!--<div class="screening position">-->
                        <!--<div class="title">-->
                            <!--<i class="s-icon icon-position"></i>-->
                            <!--<h5>场地位置</h5>-->
                            <!--<a href="javascript:;" class="icon-triangedown"></a>-->
                        <!--</div>-->
                        <!--<ul class="option-list">-->
                            <!--<li>-->
                                <!--<el-checkbox class="checkbox" checked>备选项</el-checkbox>-->
                            <!--</li>-->
                            <!--<li>-->
                                <!--<el-checkbox class="checkbox" checked>备选项</el-checkbox>-->
                            <!--</li>-->
                            <!--<li>-->
                                <!--<el-checkbox class="checkbox" checked>备选项</el-checkbox>-->
                            <!--</li>-->
                            <!--<li>-->
                                <!--<el-checkbox class="checkbox" checked>备选项</el-checkbox>-->
                            <!--</li>-->
                            <!--<li>-->
                                <!--<el-checkbox class="checkbox" v-model="checked" checked>备选项</el-checkbox>-->
                            <!--</li>-->
                        <!--</ul>-->
                    <!--</div>-->

                    <!--落位区域-->
                    <div class="screening arrArea">
                        <div class="title">
                            <i class="s-icon icon-luowei"></i>
                            <h5>落位区域</h5>
                            <a href="javascript:;" class="icon-triangedown"></a>
                        </div>
                        <el-checkbox-group v-model="arrArea">
                            <ul class="option-list">
                                <li v-for="(value,key) in searchCondition.position">
                                    <el-checkbox class="checkbox" :label="key">{{value}}</el-checkbox>
                                </li>
                            </ul>
                        </el-checkbox-group>
                    </div>

                    <!--配套服务-->
                    <div class="screening arrSort">
                        <div class="title">
                            <i class="s-icon icon-assort"></i>
                            <h5>配套服务</h5>
                            <a href="javascript:;" class="icon-triangedown"></a>
                        </div>
                        <el-checkbox-group v-model="arrSort">
                            <ul class="option-list">
                                <li v-for="(value,key) in searchCondition.facitilies">
                                    <el-checkbox class="checkbox" :label="value">{{value}}</el-checkbox>
                                </li>
                            </ul>
                        </el-checkbox-group>
                    </div>

                    <!--空间层高-->
                    <div class="screening space-height">
                        <div class="title">
                            <i class="s-icon icon-height"></i>
                            <h5>空间层高</h5>
                        </div>
                        <ul class="option-list">
                            <li>
                                <input type="number"  class="ipt-height">米 以上
                            </li>
                        </ul>
                    </div>
                </div>
                <div class="space-list fr search-list">
                    <div class="search-input-wrap clearfix">

                        <div class="clearfix">
                            <div class="fl search-ipt-wrap">
                                <i class="s-icon icon-search"></i>
                                <input @keyup.enter="getData" type="text" placeholder="请输入关键字" v-model='urlData.q.keyword'>
                            </div>
                            <router-link :to="'/search/map/?order_id='+$route.query.order_id" class="fr s-searchbtn"><i class="s-icon icon-map"></i>地图检索</router-link>
                            <!--<button class="fr s-searchbtn"><i class="s-icon icon-map"></i>地图检索</button>-->
                        </div>
                    </div>
                    <div class="list">
                        <ul class="recommend recommend-sub list-piece clearfix">
                            <li v-for="item in placeList" @click="popSearchDtl(item.id)">
                                <a href="javascript:;">
                                    <div class="img">
                                        <img onerror="javascript:this.src='/static/images/error.jpg';" :src="item.site_pictures.length > 0 ? item.site_pictures[0]['url_400_267'] : ''">
                                    </div>

                                    <div class="tag" v-if="item.second_type == '核心' || item.second_type =='自营' ">{{item.second_type}}</div>
                                    <div class="text">
                                        <h2 class="title">{{item.title}}</h2>
                                        <div class="textinfo">
                                            <p><i class="s-icon icon-reason"></i>推荐理由：{{item.recommend_reason}}</p>
                                            <p><i class="s-icon icon-adress"></i>地址：{{item.city_name}}&nbsp;{{item.district}}&nbsp;{{item.address}}</p>
                                        </div>
                                    </div>
                                    <table>
                                        <tr>
                                            <th width="32%">场地类型</th>
                                            <th width="40%">市场价</th>
                                            <th width="28%">空间数</th>
                                        </tr>
                                        <tr>
                                            <td>{{item.site_type}}</td>
                                            <td>{{item.lower_price}} <span v-if="item.lower_price !== '面议' ">起</span></td>
                                            <td>{{item.count_space}}</td>
                                        </tr>
                                    </table>
                                </a>
                            </li>
                        </ul>

                        <a id="morePlace" class="more-place" v-if="!isNoMoreData" @click="getData('more')" href="javascript:;">
                            <span>加载更多</span>
                            <i class="icon-arrowbottom"></i>
                        </a>
                        <p style="text-align: center" v-if="isNoMoreData">没有更多了...</p>
                    </div>

                </div>
            </div>

        </div>

        <el-dialog class="popSearchDtl" v-model="dialogVisible" size="large" @close="orderchange">
            <iframe src="" frameborder="0" name="popsearchdtl" id="popsearch"></iframe>
            <span slot="footer" class="dialog-footer">
                <a href="javascript:;" @click="dialogVisible = false" class="s-searchbtn dl-btn">确 定</a>
            </span>
        </el-dialog>

        <div class="listSlideUp img" @click="listSlideUp"><img src="/static/images/iconUp.png" alt="向上" /></div>
    </div>
</template>

<script>

    import Lib from 'assets/Lib.js'
    import 'assets/css/component.css';
    import 'assets/css/hold-event.css';
    import 'assets/css/search.css';
    export default {
        data() {
            return {
                checked: true,
                dialogVisible : false,
                tags :[],
                searchData : {
                    budget_amount : '',
                    area_size : '',
                    search_people:'',
                },
                searchKeyword : '',   //搜索关键词
                placeList:[],
                isNoMoreData : false,
                selectSearchReady : false,
                urlData : {
                    page : 1,
                    city_id : '',
                    tags:'',             //配套服务
                    //business_circle:'',  //活动类型
                    spaces_through_three_areas_cont: '',//落位区域
                    q : {
                        keyword: self.searchKeyword,
                        district_name_eq:'',
                        site_type_eq:'',
                        spaces_market_price_gteq:'',
                        spaces_market_price_lteq:'',
                        //spaces_area_gteq:'',
                        //spaces_area_lteq:'',
                        spaces_Max_seating_capacity_gteq:'',
                        spaces_Max_seating_capacity_lteq:'',
                        site_district_name_eq:'',
                        spaces_height_gteq:'',
                    }
                },
                arrSort:[],
                arrArea:[],
                stringArrSort:[],
                stringArrArea:[],
                chooseSpaceArr:[],
                default:[],
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
                if(s.cities){
                    var l=s.cities.length-1;
                    if(s.cities[l].name!=='不限'){
                        s.cities.push({name:'不限',id:''})
                        setTimeout(function () {
                            self.selectSearchReady = true
                        },300)
                    }
                }
                if(s.activity_type){
                    s.activity_type['不限'] = ''
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
            spaceManageSelectCount () {
                return this.$store.state.spaceManageSelectCount
            },
            spaceManageSelectList () {
                return this.$store.state.spaceManageSelectList
            },
            order_id(){
                return this.$route.query.order_id
            }
        },
        beforeMount(){
            this.$store.commit('changeShowHeader',false) // 隐藏头部
            this.$store.commit('changeShowFooter',false) // 隐藏尾部部
        },
        mounted () {
            this.$store.commit('getSpaceManageList') // 获取本地保存提交的数据
            var self = this;
            if(self.$route.query.order_id){
                $.ajax({
                    url: window.YUNAPI.host + 'api/sites/get_search_default.json',
                    data : {
                        order_id : self.$route.query.order_id
                    },
                    success: function (data) {
                        self.default=data.default_condition;
                        //self.urlData.business_circle=self.default.activity_type;
                        self.searchData.budget_amount=self.default.budget_amount;
                        self.urlData.city_id=self.default.city;
                        self.searchData.search_people=self.default.search_people;

                        self.getData();
                    }
                });
            }else {
                self.getData();
            }

            $('.screening .title').on('click',function () {
                self.slideUpDown($(this));
            });
        },
        components: {},
        methods: {
            //选择弹窗里的空间后，提交数目更新
            orderchange(){
                this.$store.commit('getSpaceManageList');
            },

            //场地详情弹窗
            popSearchDtl(e){
                var self = this;
                var newHref = 'http://'+window.location.host+'/search/dtl/'+e+'?order_id='+self.order_id;
                self.dialogVisible = true;
                setTimeout(function () {
                    document.getElementById('popsearch').contentWindow.location.href = newHref;
                },300);
            },

            //置顶
            listSlideUp(){
                $('html,body').animate({scrollTop:0},300);
            },

            //左边栏筛选项 展开/折叠
            slideUpDown(e){
                var optionList=e.parents('.screening').find('.option-list');
                var triangedown=optionList.parents('.screening').find('.icon-triangedown');
                optionList.toggleClass('slidedown');
                triangedown.toggleClass('triange');
            },

            //弹窗提示
            noSpaceOpen() {
                this.$message('请选择适合的场地后进行提交!');
            },

            //提交
            spaceSubmit() {
                var self = this;
                if(self.spaceManageSelectCount==0){
                    //请选择适合的场地后进行提交
                    self.noSpaceOpen();
                    return;
                }
                this.$msgbox({
                    message: '确认提交空间？',
                    showCancelButton: true,
                    confirmButtonText: '确定',
                    cancelButtonText: '取消'
                }).then(action => {
                    if(action=='confirm'){
                        $('input[name=chooseSpace]:checked').each(function () {
                            self.chooseSpaceArr.push($(this).val());
                        });
                        $.post({
                            url: window.YUNAPI.siteRecommend,
                            data: {
                                space_ids : self.spaceManageSelectList,
                                order_id : self.$route.query.order_id
                            },
                            success:function (data) {
                                //console.log(self.chooseSpaceArr);
                                self.$message({
                                    type: 'success',
                                    message: '提交成功'
                                });
                                self.$store.commit('spaceManageChange',[]) //提交成功 清空本地保存的数据
                                //关闭当前页面（target="_blank"打开的页面管用）
                                window.opener=null;
                                window.open('','_self');
                                window.close();
                            }
                        });
                    }
                });
            },


            getData(type){
                var self= this;
                if( this.placeMore && this.placeMore.state() == 'pending'){
                    return
                }
                self.$store.commit('loading',true);
                //落位区域-分割
                self.stringArrArea=self.arrArea.join(',');
                //配套服务-分割
                self.stringArrSort=self.arrSort.join(',');

                //urlData.tags值(配套服务+活动类型)
                if(self.stringArrSort){
                    self.stringArrSort=self.stringArrSort+','
                }
                self.urlData.tags = self.stringArrSort
                        //+self.urlData.business_circle;
                //落位区域值
                self.urlData.spaces_through_three_areas_cont = self.stringArrArea

                //空间层高值
                self.urlData.q.spaces_height_gteq = $('.space-height .ipt-height').val();
                $('.space-height .ipt-height').val('');  //清零

                //参数
                if(type == 'more'){
                    self.urlData.page++;
                    $('#morePlace span').text('正在加载...')
                }

                //搜索 容纳人数
                if(self.searchData.search_people){
                    var search_people = self.searchData.search_people.split('-')
                    self.urlData.q.spaces_Max_seating_capacity_gteq = search_people[0]
                    self.urlData.q.spaces_Max_seating_capacity_lteq = search_people[1]
                }else{
                    self.urlData.q.spaces_Max_seating_capacity_lteq = ''
                    self.urlData.q.spaces_Max_seating_capacity_lteq = ''
                }

                //搜索 预算范围
                if(self.searchData.budget_amount){
                    var budget_amount = self.searchData.budget_amount.split('-')
                    self.urlData.q.spaces_market_price_gteq = budget_amount[0]
                    self.urlData.q.spaces_market_price_lteq = budget_amount[1]
                }else{
                    self.urlData.q.spaces_market_price_gteq = ''
                    self.urlData.q.spaces_market_price_lteq = ''
                }

                //搜索 面积限制
//                if(self.searchData.area_size){
//                    var area_size = self.searchData.area_size.split('-')
//                    self.urlData.q.spaces_area_gteq = area_size[0]
//                    self.urlData.q.spaces_area_lteq = area_size[1]
//                }else{
//                    self.urlData.q.spaces_area_gteq = ''
//                    self.urlData.q.spaces_area_lteq = ''
//                }


                self.placeMore = $.ajax({
                    url: window.YUNAPI.host + 'api/sites/search',
                    data : self.urlData,
                    success: function (data) {

                        if(type == 'more'){
                            self.placeList=self.placeList.concat(data.sites);
                        }else{
                            self.placeList=data.sites
                        }

                        if(data.sites.length < self.$store.state.pageSize){
                            self.isNoMoreData = true
                        }else{
                            self.isNoMoreData = false
                        }

                        self.$store.commit('loading',false);
                        $('#morePlace span').text('加载更多')
                    },
                    error: function (data) {
                        $('#morePlace span').text('加载更多')
                    }
                });

            },

        }
    }
</script>

<style scoped>
    html{background: #fff;}
</style>





