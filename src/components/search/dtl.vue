
<template>
    <div class="pagination-fore-end" style="background: #fff;padding-top: 20px">
        <div class="w800 searchdtl clearfix">
            <div class="fl evdtlcont">
                <div class="title">
                    <h2>{{placeDtl.title}}</h2>
                </div>
                <div class="textinfo">
                    <p><i class="s-icon icon-reason"></i>推荐理由：{{placeDtl.recommend_reason}}</p>
                    <p><i class="s-icon icon-adress"></i>地址：{{placeDtl.city_name}} {{placeDtl.district}} {{placeDtl.address}}</p>
                </div>

                <ul class="dtl-list">
                    <li class="clearfix arrsort">
                        <h5>场地配套</h5>
                        <!--<div class="option-list dtl">-->
                            <!--<el-checkbox-group v-model="checkList">-->
                                <!--<el-checkbox v-for="item in arrSort" :label="item" class="checkbox"></el-checkbox>-->
                            <!--</el-checkbox-group>-->
                        <!--</div>-->
                        <p v-for="item in arrSort">{{item}}</p>
                    </li>
                    <li class="fl mr20 clearfix">
                        <h5>人数</h5>
                        <p><span>最大容纳</span>{{placeDtl.max_people}}人</p>
                    </li>
                    <li class="clearfix">
                        <h5>场地面积</h5>
                        <p><span>面积</span>{{placeDtl.max_size}}平方</p>
                    </li>
                    <li class="clearfix">
                        <h5>报价</h5>
                        <p><span>报价名称</span>常规</p>
                        <p><span>市场价</span>{{placeDtl.lower_price}} <span v-if="placeDtl.lower_price !== '面议' ">起</span></p>
                        <p><span>预订须知</span>{{placeDtl.booking_notes}}</p>
                    </li>
                    <li class="clearfix">
                        <h5>联系人</h5>
                        <p><span>联系人</span>{{placeDtl.contact}}</p>
                        <p><span>联系电话</span>{{placeDtl.phone}}</p>
                        <p><span>联系邮箱</span>{{placeDtl.email}}</p>
                    </li>
                </ul>
            </div><!--evdtlcont-end-->
            <div class="fr evdtllist">
                <div class="title">
                    <i class="s-icon icon-space"></i>
                    <p>拥有<span class="green"> {{placeDtl.count_space}} </span>个空间</p>
                </div>
                <div class="cont">
                    <dl>
                        <dt>活动类型</dt>
                        <dd>
                            {{placeDtl.service_type}}
                        </dd>
                    </dl>
                    <dl>
                        <dt>场地类型</dt>
                        <dd>
                            {{placeDtl.site_type}}
                        </dd>
                    </dl>
                </div>
            </div><!--evdtllist-end-->
        </div>
        <div class="w800 mt20 space-list dtl search-list">
            <div class="list">
                <ul class="recommend recommend-sub list-piece clearfix">
                    <li v-for="(item,index) in site_spaces">
                        <a class="img" :href="'/space/'+item.id" target="_blank">
                            <img onerror="javascript:this.src='/static/images/error.jpg';" :src="item.img_paths.length > 0 ? item.img_paths[0]['url_400_267'] : ''">
                        </a>
                        <div class="tag" v-if="item.keyword == '核心' || item.keyword =='自营' ">{{item.keyword}}</div>
                        <div class="text">
                            <a target="_blank" class="title" :href="'/space/'+item.id">{{item.name}}</a>
                            <div class="textinfo">
                                <p><i class="s-icon icon-reason"></i>推荐理由：{{item.reasons}}</p>
                                <p><i class="s-icon icon-adress"></i>落位区域：{{item.through_three_areas}}</p>
                            </div>
                        </div>
                        <table>
                            <tr>
                                <th width="30%">最大容纳</th>
                                <th width="30%">空间面积</th>
                                <th width="40%">市场价</th>
                            </tr>
                            <tr>
                                <td>{{item.Max_seating_capacity}}人</td>
                                <td>{{item.area}} ㎡</td>
                                <td>{{item.market_price}} <span v-if="item.market_price !== '面议' ">起</span></td>
                            </tr>
                        </table>
                        <div class="option-list">
                            <label >
                                <input @change="spaceManageSelectChange($event)" type="checkbox" name="chooseSpace" class="checkbox" :value="item.id" :checked="isInArray(spaceManageSelectList,item.id)">
                                <span>选择</span>
                            </label>
                            <!--<el-checkbox name="chooseSpace" class="checkbox" v-model="item.id" :value="item.id">选择</el-checkbox>-->
                        </div>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>

    function removeByValue(arr, val) {
        for(var i=0; i<arr.length; i++) {
            if(arr[i] == val) {
                arr.splice(i, 1);
                break;
            }
        }
    }

    import Lib from 'assets/Lib.js'
    import 'assets/css/component.css';
    import 'assets/css/hold-event.css';
    import 'assets/css/search.css';
    export default {
        data() {
            return {
                checked: true,
                tags :[],
                site_spaces: [],
                checkList: [],
                placeDtl: [],
                arrSort:[],
                searchData : {
                    space_type : '',
                    area_size : '',
                    budget_amount : ''

                },
                selectSearchReady : false,
                chooseSpace : {is:false},
                chooseSpaceArr:[],
                orderNumbs:2,

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
            spaceManageSelectCount () {
                return this.$store.state.spaceManageSelectCount
            },
            spaceManageSelectList () {
                return this.$store.state.spaceManageSelectList
            },

        },
        beforeMount(){
            this.$store.commit('changeShowHeader',false) // 隐藏头部
            this.$store.commit('changeShowFooter',false) // 隐藏尾部部
        },
        mounted () {
            var self = this;
            self.$store.commit('loading',true);
            this.$store.commit('getSpaceManageList') // 获取本地保存提交的数据
            if(typeof this.$route.query.q != 'undefined'){
                this.spaceSearchCondition.q.keyword = this.$route.query.q
                self.spaceSearchCondition.city_id = self.$store.state.city_id
            }

            if(typeof this.$route.query.site_site_type_eq != 'undefined'){
                this.spaceSearchCondition.q.site_site_type_eq = this.$route.query.site_site_type_eq
            }

            $.ajax({
                url: window.YUNAPI.host + 'api/sites/' + this.$route.params.id,
                data : self.urlData,
                success: function (data) {
                    //console.log(data,666)
                    self.placeDtl=data.site;
                    self.site_spaces=data.site_spaces;

                    //场地配套
                    if(self.placeDtl.facilities){
                        self.arrSort=self.placeDtl.facilities.split(',');
                    }
                    self.$store.commit('loading',false);
                }
            });

//            var storage=window.localStorage;
//            storage.a=('11111');
//            storage['a']=('66666');
//            storage.setItem('aaa','999')
//            storage.getItem('aaa')
//            storage.removeItem('aaa')
//            console.log(storage.getItem('aaa'));

        },
        components: {},
        methods: {
            //弹窗提示
            noSpaceOpen() {
                this.$message('请选择适合的场地后进行提交！');
            },

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

            spaceManageSelectChange(e){
//                console.log(e.target.value)
//                console.log(e.target.checked)
                var array = LS.get('spaceManageSelect')
                if(!array){
                    array = []
                }
                if(e.target.checked){
                    array.push(e.target.value)
                }else{
                    removeByValue(array,e.target.value)
                }
                //console.log(array)
                this.$store.commit('spaceManageChange',array)
            },
            isInArray(arr,val){
                for(var i=0; i<arr.length; i++) {
                    if(arr[i] == val) {
                        return true
                    }
                }
                return false
            }
        }
    }
</script>

<style scoped>
    .search-list li .option-list label{
        display: block;
        margin-top: 6px;
    }
    input[name='chooseSpace']{
        width: 15px;
        height: 15px;
    }
    body,html{
        background: #fff;
    }

</style>





