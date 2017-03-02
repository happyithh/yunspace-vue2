<template>
    <div>
        <div class="w1200 booking-container clearfix mt30">
            <!--预定订单详情-->
            <div class="fl booking-left collt">
                <h2>询价清单</h2>

                <ul class="collt-list">
                    <li class="clearfix" v-for="(v,k) in inquiryList">
                        <p class="fl">{{v}}</p>
                        <el-checkbox v-model="inquiryListChange[k]" class="fr checkbox" ></el-checkbox>
                        <!--<input v-model="inquiryListChange[k]" type="checkbox">-->
                        <!--<checkbox></checkbox>-->
                    </li>
                </ul>

            </div>

            <!--预定信息填写-->
            <form action="" class="clearfix" id="inquiryForm">
                <div class="fr booking-right collt">
                    <h2>基本信息</h2>
                    <div class="evformbox">
                        <div class="mainbox">
                            <ul class="inputbox">
                                <li class="inputwrap clearfix">
                                    <div class="text"><span class="red">*</span>您的称呼：</div>
                                    <input class="fminput" v-model="inquiryData.contact" name="username" data-rule-required="true" data-msg-required="请输入您的真实姓名!" placeholder="请输入您的真实姓名!">
                                </li>
                                <li class="inputwrap clearfix">
                                    <div class="text">公司名称（选填）：</div>
                                    <input class="fminput" v-model="inquiryData.company" name="company" placeholder="请输入您的公司名称!">
                                </li>
                                <li class="inputwrap clearfix">
                                    <div class="text"><span class="red">*</span>您的联系方式：</div>
                                    <input class="fminput" v-model="inquiryData.phone" name="phone" type="text" data-msg-required="请输入您的联系方式!" placeholder="请输入11位手机号" />
                                </li>
                                <li class="inputwrap clearfix">
                                    <div class="text"><span class="red">*</span>短信验证码：</div>
                                    <input v-model="inquiryData.auth_code" class="fminput" type="text" placeholder="请输入6位数验证码" data-rule-required="true" data-msg-required="请输入验证码!"/>
                                    <button type="button" id="inquirySendCode" class="sendcode" @click="sendPhoneCode($event)">发送验证码</button>
                                </li>
                            </ul>
                        </div>
                        <h2 class="mt20">您的计划</h2>
                        <div  class="mainbox">
                            <ul class="inputbox">

                                <li class="inputwrap clearfix">
                                    <div class="text"><span class="red">*</span>活动时间：</div>
                                    <div class="fl time timedate">
                                        <el-date-picker
                                                v-model="inquiryData.time"
                                                type="daterange"
                                                placeholder="选择日期范围"
                                                format="yyyy年MM月dd"
                                                style="width: 300px">
                                        </el-date-picker>
                                    </div>
                                </li>

                                <li class="inputwrap inputsex clearfix">
                                    <div class="text"><span class="red"></span>可改期：</div>
                                    <div class="yes sexwrap">
                                        <el-radio class="radio" v-model="inquiryData.change_time" label="1">是</el-radio>
                                    </div>
                                    <div class="no sexwrap">
                                        <el-radio class="radio" v-model="inquiryData.change_time" label="0">否</el-radio>
                                    </div>
                                </li>

                                <li class="inputwrap clearfix">
                                    <div class="text">活动人数：</div>
                                    <!--<input class="fminput" type="text" placeholder="请输入项目计划落地城市" />-->
                                    <div class="result fminput">
                                        <el-select v-model="inquiryData.number_of_activities" placeholder='请选择活动人数'>
                                            <el-option
                                                    v-for="(value,key) in searchCondition.activity_people"
                                                    :label="value"
                                                    :value="key">
                                            </el-option>
                                        </el-select>
                                    </div>
                                </li>

                                <li class="inputwrap clearfix">
                                    <div class="text">活动预算：</div>
                                    <!--<input class="fminput" type="text" placeholder="请输入项目计划落地城市" />-->
                                    <div class="result fminput">
                                        <el-select v-model="inquiryData.budget_amount" placeholder='请选择您的预算范围'>
                                            <el-option
                                                    v-for="(value,key) in searchCondition.budget_amount"
                                                    :label="value"
                                                    :value="key">
                                            </el-option>
                                        </el-select>
                                    </div>
                                </li>

                                <li class="inputwrap clearfix">
                                    <div class="text">活动类型：</div>
                                    <!--<input class="fminput" type="text" placeholder="请输入项目计划落地城市" />-->
                                    <div class="result fminput">
                                        <el-select v-model="inquiryData.activity_type" placeholder='请选择活动类型'>
                                            <el-option
                                                    v-for="(value,key) in searchCondition.activity_type"
                                                    :label="value"
                                                    :value="key">
                                            </el-option>
                                        </el-select>
                                    </div>
                                    <!--<input style="visibility: hidden" name="city" v-model="demand.city" type="text" data-rule-required="true" data-msg-required="请选择城市!">-->
                                </li>

                                <li class="inputwrap trea clearfix">
                                    <div class="text">其他要求：</div>
                                    <textarea v-model="inquiryData.activities_required" rows="8" placeholder="请填写更多的详细信息，帮助您快速找到适合的场地。"></textarea>
                                </li>
                            </ul>
                            <button class="evform-btn" type="button" @click="submitInquiry">提交</button>
                        </div><!--表单mainbox-end-->
                    </div>

                    <!--状态弹窗-->
                    <div class="formstate-wp" v-show="showstate && !showmask">
                        <div class="mask-bg" @click="showstate=!showstate"></div>
                        <div class="formstate">
                            <h2>提交成功</h2>
                            <p>我们将在30分钟内和您取得联系<br>
                                请注意接听来电</p>
                        </div>
                    </div>

                </div><!--right-end-->
            </form>
        </div>
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
                shownumbs: 0,
                showtype: 0,
                showcitys: 0,
                showstate:0,
                bugdets:[1,2,3],
                showbugdets:0,

                inquiryData : {
                    contact : '',
                    auth_code : '',
                    company : '',
                    phone : '',
                    s_time : '',
                    e_time : '',
                    ip_city : '' ,
                    number_of_activities : "50",
                    budget_amount : '',
                    activity_type : '零售短租',
                    source : '',
                    activities_required : '',
                    time : ['',''],
                    change_time : '1',
                    order_city:'上海',
                    source:'询价'
                },

                inquiryListChange : {},
                submitPromise : ''

            }
        },
        components: {

        },
        computed : {
            searchCondition (){
                return this.$store.state.searchCondition
            },
            inquiryCount () {
                return this.$store.state.inquiryCount
            },
            inquiryList () {
                return this.$store.state.inquiryList
            },
//            inquiryListChange : {
//                get: function () {
//                    var e = {}
//                    for( var i in this.inquiryList){
//                        e[i] = true
//                    }
//                    return e
//                },
//                // setter
//                set: function (newValue) {
//                    console.log(newValue)
//                }
//            },
            selectInquiryIds () {
                var e = []
                for (var i in this.inquiryListChange){
                    if(this.inquiryListChange[i]){
                        e.push(i)
                    }
                }
                return e;
            },
            personalData (){
                return this.$store.state.personalData
            }
        },
        mounted () {
            var self = this;
            setTimeout(function () {
                GlobleFun.validate("#inquiryForm");
                if(self.personalData.name){
                    self.inquiryData.phone = self.personalData.mobile
                    self.inquiryData.contact = self.personalData.name
                    self.inquiryData.company = self.personalData.company_name
                }
            },300)

            this.$store.commit('loading',false)

            if(self.inquiryCount < 1){
                APP.$message({
                    message: "请先添加询价空间",
                    type: 'warning',
                    duration : 2000
                });
                router.back()
            }

            //获取 询价 列表
            var e = {}
            for( var i in this.inquiryList){
                e[i] = true
            }
            this.inquiryListChange = e;
        },
        methods: {
            sendPhoneCode : function (e) {
                var self = this;
                var success = function (data) {
                    self.inquiryData.code_token = data.data;
                };
                GlobleFun.sendPhoneCode(this.inquiryData.phone,success,e.target);
                return false
            },
            submitInquiry : function () {
                if(!this.personalData.uid){
                    this.$parent.showForm.login = true
                    return
                }

                var self = this;
                var isValid = $("#inquiryForm").valid();

                if(!isValid) return

                if(!this.inquiryData.time[0]){
                    this.$message({
                        message: "请选择日期",
                        type: "error",
                        duration : 2000
                    });
                    return
                }
                if(this.selectInquiryIds.length <= 0){
                    this.$message({
                        message: "请先添加询价空间",
                        type: "error"
                    });
                    return
                }
                //询价必须数据
                this.inquiryData.space_ids = this.selectInquiryIds
                this.inquiryData.uid = this.personalData.uid
                this.inquiryData['access-token'] = this.personalData.access_token
                this.inquiryData.client= this.personalData.client

                this.inquiryData.order_city = $('#cityId input').val() // 需求单城市

                if(!self.inquiryData.time[0]){
                    self.$message({
                        message: '活动时间不能为空',
                        type: 'warning',
                        duration : 2000
                    });
                    return
                }

                var sd = new Date(this.inquiryData.time[0]);
                var ed = new Date(this.inquiryData.time[1]);
                this.inquiryData.s_time = sd.getFullYear() + '-' + (sd.getMonth() + 1) + '-' + sd.getDate() ;
                this.inquiryData.e_time = ed.getFullYear() + '-' + (ed.getMonth() + 1) + '-' + ed.getDate() ;

                if( self.submitPromise && self.submitPromise.state() == 'pending'){
                    return
                }

                self.submitPromise = $.post({
                    url: window.YUNAPI.createInquiry,
                    data : self.inquiryData,
                    success : function (data) {

                        if(data.status == 1){
                            router.replace('/personal/enquiry')
                            self.$store.commit('inquiryClear');
                        }

                        if(data.status == -5){ //需要重新登录
                            self.$store.commit('personalDataChange',{});//保存个人信息
                        }

                        GlobleFun.httpMessage(data);

                    }
                });

            }
        },

        //记住密码
        rememberPassword(){}
    }

</script>






