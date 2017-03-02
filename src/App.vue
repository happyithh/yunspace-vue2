<template>
    <div id="app2" v-on:click="bodyClick">
        <module-header v-show="showHeader" cities = "cities" v-on:toggleLoginForm ="toggleLoginForm"></module-header>

        <!--<router-view></router-view>-->
        <div v-loading="loading" class="el-loading-yun"></div>
        <div v-if="loading" class="loading-bg"></div>

        <router-view  class="child-view"></router-view>

        <module-footer v-show="showFooter" ref="test" v-if="!loading"></module-footer>

        <div v-if="httpError">
            请求错误
            <button>刷新页面</button>
        </div>

        <!--app下载-->
        <el-dialog v-model="showForm.showApp" size="tiny">
            <div class="appcode-wrap">
                <div class="pserson-code-title">
                    <span>扫一扫</span>
                </div>
                <div class="code-img">
                    <p class="code-title">云SPACE场地大师<br>空间场地管理App</p>
                    <img src="http://s2.yunspace.com.cn/package/Web_Static_4.0/interface/assets/img/ygj_new.png" alt="" width="100" height="100">
                </div>
            </div>
        </el-dialog>


        <!--注册-->
        <el-dialog v-model="showForm.reg" @open="regOpen">
            <!--regbox注册-开始-->
            <div class="loginreg-box">
                <div class="regbox">
                    <h2>注册</h2>
                    <form action="" id="regForm">
                        <div class="mainbox">
                            <ul class="inputbox">
                                <li class="logregwrap">
                                    <span class="text">姓</span>
                                    <!--<input class="logreginput" type="text" placeholder="请输入您的姓氏" />-->
                                    <input class="logreginput" v-model="regData.surname" name="surname" data-rule-required="true" data-msg-required="请输入您的姓氏!" placeholder="请输入您的姓氏">
                                </li>
                                <li class="logregwrap">
                                    <span class="text">名</span>
                                    <!--<input class="logreginput" type="text" placeholder="请输入您的名称" />-->
                                    <input class="logreginput" v-model="regData.username" name="username" data-rule-required="true" data-msg-required="请输入您的名称!" placeholder="请输入您的名称">
                                </li>
                                <li class="logregwrap">
                                    <span class="text">手机号</span>
                                    <input autocomplete="off" class="logreginput" v-model="regData.mobile" name="phone" type="text" data-msg-required="请输入您的联系方式!" placeholder="请输入正确的11位手机号码" />
                                </li>
                                <li class="logregwrap">
                                    <span class="text">验证码</span>
                                    <!--<input class="logreginput" type="text" placeholder="" />-->
                                    <input class="logreginput" v-model="regData.auth_code" name="auth_code" data-rule-required="true" data-msg-required="请输入验证码!" placeholder="请输入验证码">
                                    <button class="sendcode" type="button" @click="sendPhoneCode">发送验证码</button>
                                </li>
                                <li class="logregwrap">
                                    <span class="text">设置密码</span>
                                    <!--<input class="logreginput" type="text" placeholder="密码长度不能少于6位，不能包含空格" />-->
                                    <input autocomplete="off" type="password" class="logreginput" v-model="regData.password" name="password" data-rule-required="true" data-msg-required="请输入密码!" placeholder="密码长度不能少于6位，不能包含空格">
                                    <!--<i class="icons icon-passwordhide"></i>-->
                                </li>
                                <li class="logregwrap">
                                    <span class="text">确认密码</span>
                                    <input autocomplete="off" type="password" class="logreginput" v-model="regData.password_confirmation" name="password_confirmation" data-rule-required="true" data-msg-required="请输入确认密码!" placeholder="请输入确认密码">
                                    <!--<input class="logreginput" type="password" placeholder="" />-->
                                </li>
                            </ul>
                            <button class="logreg-btn" type="button" @click="submitReg">立即注册</button>

                            <div class="repasswordbox">
                                <a class="back" href="javascript:;" @click="showForm.login = true"><span class="icon-arrowleft"></span>返回</a>
                            </div>
                        </div>
                    </form>
                </div><!--regbox注册-结束-->
            </div>

        </el-dialog>
        <!--登陆-->
        <el-dialog v-model="showForm.login" @open="loginFormOpen">
            <!--regbox注册-开始-->
            <div class="loginreg-box">
                <form action="" id="loginForm">
                    <!--loginbox登录-开始-->
                    <div class="loginbox">
                        <h2>登录</h2>
                        <div class="mainbox">
                            <ul class="inputbox">
                                <li class="logregwrap">
                                    <input class="logreginput" v-model="loginData.mobile" name="phone" type="text" data-msg-required="请输入您的联系方式!" placeholder="请输入11位手机号" />
                                    <!--<div class="warning"><i class="icons icon-warning"></i>请输入正确的11位手机号码</div>-->
                                </li>
                                <li class="logregwrap">
                                    <input class="logreginput" type="password" v-model="loginData.password" name="password" data-rule-required="true" data-msg-required="请输入密码!" placeholder="请输入密码!">
                                    <!--<i class="icons icon-passwordshow"></i>-->
                                </li>
                            </ul>

                            <div class="rememberbox clearfix">
                                <div class="fl remember clearfix">
                                    <label>
                                        <input v-model="isRememberPhone" class="fl checkbox" type="checkbox" value="记住手机号码">
                                        <p class="fr">记住手机号码</p>
                                    </label>
                                </div>
                                <a class="fr forget" href="javascript:;" @click="showForm.forgetPassword = true">忘记密码？</a>
                            </div>

                            <button class="logreg-btn" type="button" @click="login">登录</button>
                        </div>
                        <div class="hreftext clearfix">
                            <a class="fl" href="javascript:;" @click="showForm.reg = true">创建账号</a>
                            <a class="fr" href="javascript:;" @click="showForm.authLogin = true">验证码登录</a>
                        </div>

                        <!--<div class="log-thirdparty">-->
                            <!--<div class="title">-->
                                <!--<div class="line"></div>-->
                                <!--<h5>或通过以下方式快速登录</h5>-->
                            <!--</div>-->
                            <!--<ul class="thirdparty clearfix">-->
                                <!--<li><a class="wechat" href="javascript:;"></a> </li>-->
                                <!--<li><a class="sina" href="javascript:;"></a></li>-->
                                <!--<li><a class="qq" href="javascript:;"></a></li>-->
                            <!--</ul>-->
                        <!--</div>-->
                    </div><!--loginbox登录-结束-->
                </form>
            </div>

        </el-dialog>
        <!--忘记密码-->
        <el-dialog v-model="showForm.forgetPassword" @open="forgetPasswordFormOpen" @close="forgetPasswordClose">
            <!--regbox注册-开始-->
            <div class="loginreg-box">
                <form action="" id="forgetPasswordForm">
                    <!--loginbox登录-开始-->
                    <div class="repasswordbox" v-if="changePassWordStep == 1">
                        <h2>找回密码</h2>
                        <div class="mainbox">
                            <ul class="inputbox">
                                <li class="logregwrap">
                                    <input v-model="changePassWordData.mobile" class="logreginput" type="text" placeholder="手机号" />
                                </li>
                                <li class="logregwrap">
                                    <input v-model="changePassWordData.auth_code" class="logreginput" type="text" placeholder="验证码" />
                                    <button class="sendcode" type="button" @click="sendChangePasswordCode">发送验证码</button>
                                </li>
                            </ul>

                            <button class="logreg-btn" type="button" @click="changePasswordNext">下一步</button>
                        </div>
                        <a class="back" href="javascript:;" @click="showForm.login = true"><span class="icon-arrowleft"></span>返回</a>
                    </div><!--找回密码-结束-->

                    <div class="repasswordbox" v-if="changePassWordStep == 2">
                        <h2>重置密码</h2>
                        <div class="mainbox">
                            <ul class="inputbox">
                                <li class="logregwrap">
                                    <input v-model="changePassWordData.password" class="logreginput" type="password" placeholder="新密码" />
                                    <i class="icon passwordshow"></i>
                                </li>
                                <li class="logregwrap">
                                    <input v-model="changePassWordData.password_confirmation" class="logreginput" type="password" placeholder="确认密码" />
                                    <i class="icon passwordshow"></i>
                                </li>
                            </ul>

                            <button class="logreg-btn" type="button" @click="changePasswordNow">立即重置</button>
                        </div>
                        <a class="back" href="javascript:;" @click="changePassWordStep = 1"><span class="icon-arrowleft"></span>返回</a>
                    </div><!--重置密码repasswordbox-结束-->
                </form>
            </div>

        </el-dialog>
        <!--验证码登陆-->
        <el-dialog v-model="showForm.authLogin" @open="authLoginFormOpen">
            <div class="loginreg-box">
                <form action="" id="authLoginForm">
                    <div class="loginbox">
                        <h2>验证码登录</h2>
                        <div class="mainbox">
                            <ul class="inputbox">
                                <li class="logregwrap">
                                    <input class="logreginput" v-model="authLoginData.mobile" name="phone" type="text" data-msg-required="请输入您的联系方式!" placeholder="请输入11位手机号" />
                                    <!--<div class="warning"><i class="icons icon-warning"></i>请输入正确的11位手机号码</div>-->
                                </li>
                                <li class="logregwrap">
                                    <input class="logreginput" v-model="authLoginData.auth_code" name="auth_code" type="text" data-msg-required="请输入验证码!" placeholder="请输入验证码" />
                                    <button type="button" class="sendcode" id="sendAuthLoginPhoneCode" @click="sendAuthLoginPhoneCode">发送验证码</button>
                                </li>
                            </ul>

                            <div class="rememberbox clearfix">
                                <!--<div class="fl remember clearfix">-->
                                    <!--<label>-->
                                        <!--<input class="fl checkbox" type="checkbox" value="记住手机号码">-->
                                        <!--<p class="fr">记住手机号码</p>-->
                                    <!--</label>-->
                                <!--</div>-->
                            </div>

                            <button class="logreg-btn" type="button" @click="authLogin">登录</button>
                        </div>
                        <div class="hreftext clearfix">
                            <a class="fl" href="javascript:;" @click="showForm.reg = true">创建账号</a>
                            <a class="fr" href="javascript:;" @click="showForm.login = true">密码登录</a>
                        </div>

                        <!--<div class="log-thirdparty">-->
                            <!--<div class="title">-->
                                <!--<div class="line"></div>-->
                                <!--<h5>或通过以下方式快速登录</h5>-->
                            <!--</div>-->
                            <!--<ul class="thirdparty clearfix">-->
                                <!--<li><a class="wechat" href="javascript:;"></a> </li>-->
                                <!--<li><a class="sina" href="javascript:;"></a></li>-->
                                <!--<li><a class="qq" href="javascript:;"></a></li>-->
                            <!--</ul>-->
                        <!--</div>-->
                    </div><!--loginbox登录-结束-->
                </form>
            </div>

        </el-dialog>

    </div>
</template>

<script>
    import Hello from './components/Hello'
    import ModuleFooter from './components/module-footer.vue'
    import ModuleHeader from './components/module-header.vue'
    import 'assets/css/logreg.css';

    //const host = "http://api.yunspace.com.cn/";
    //const host = "http://172.16.0.141:3000/";
    const host = "http://172.16.0.145/"

    window.YUNAPI = {
        host: host,
        cities : host + 'api/cities',
        homeIpProject : host + 'api/projects/get_home_list',
        home : host + 'api/index',
        homeSearch : host + 'api/tags/get_home_search',
        article : host + 'api/informations',
        articleTags : host + 'api/tags/get_information_tags',
        articleHot : host + 'api/informations/get_hot_recommend',
        articleKeyword : host + 'api/informations/get_keyword',
        findIp : host + 'api/projects/ip_project',
        ipList : host + 'api/projects',
        active : host + 'api/activities',
        submitConsult : host + 'api/consults',
        submitHoldEvent : host + 'api/demands',
        sendPhoneCode : host + 'api/auth_codes/send_code',
        openShop : host + 'api/informations/get_retail',
        SpaceList: host + 'api/spaces',
        SpaceDtl: host + 'api/spaces',
        placeDtl : host + 'api/sites',
        feedBack: host + 'api/feedback',
        inquiry: host + 'api/demands/create_inquiry',
        collection: host + 'api/follows',
        login : host + 'api/auth/sign_in',
        register : host + 'api/auth',
        tags : host + 'api/tags/all_tags',
        createInquiry : host + 'api/demands/create_inquiry',
        createBooking : host + 'api/demands/create_booking',
        inquiryContent : host + 'api/demands/',
        spaceDtlOnly : host + 'api/spaces/detail',
        changeCollect : host + 'api/follows',
        articleZan : host + 'api/informations/add_like_amount',
        cityHotKeyword : host + 'api/tags/get_hot_keyword',
        siteRecommend : host + 'api/site_recommend_records'
    };
    export default {
        name: 'app',
        data(){
            return {
//                cities:[],
                activityType : [],
                searchCondition : [],
                isShowHomeSearchCondition : false,
                loading: true,
                httpError:false,
                cdVisible : false,  // 合作咨询的弹出框 是否显示
                showRegForm : false,
                showApp : false,
                showForm : {
                    reg : false,
                    login : false,
                    forgetPassword : false,
                    authLogin : false,
                    showApp : false
                },
                loginData : {
                    mobile : '',
                    password : ''
                },
                regData : {
                    mobile : '',
                    password : '',
                    password_confirmation : '',
                    auth_code : '',
                    code_token : '',
                    familyName : '',
                    username : '',
                    surname : ''
                },
                authLoginData : {
                    auth_code : '',
                    sign_in_type : 'sms',
                    mobile : '',
                    code_token : ''
                },
                changePassWordData : {
                    type : 'sms',
                    mobile : '',
                    code_token : '',
                    auth_code : '',
                    password : '',
                    password_confirmation : ''
                },
                changePassWordStep : 1,
                isRememberPhone : true
//                cities : window.store.state.cities
            }

        },
        computed: {
            cities (){
                return this.$store.state.cities
            },
            personalData (){
                return this.$store.state.personalData
            },
            loading(){
                return this.$store.state.loading
            },
            showHeader(){
                return this.$store.state.showHeader
            },
            showFooter(){
                return this.$store.state.showFooter
            }
        },
        components: {
            Hello, ModuleFooter, ModuleHeader
        },
        mounted () {
            var self = this;
//            console.log(window.YUNAPI);

            self.loginData.mobile = LS.get('loginPhone')

            self.$store.commit('getSelectedCity');

            $.ajax({
                url: window.YUNAPI.tags, context: document.body, success: function (data) {
//                    self.searchCondition = data;
                    self.$store.state.searchCondition = data;
//                    self.$store.state.cities = [{id:'',name:"全国"}]
//                    self.$store.state.cities = self.$store.state.cities.concat(data.cities);
                    self.$store.state.cities = data.cities
//                    self.$store.commit('searchCondition', data)
//                    self.activityType = data.activity_type;
                }
            });


        },
        methods: {
            //获取活动人数、类型
            bodyClick : function (event) {

                //搜索 : 做什么  点击其他地方隐藏
                var e = event || window.event;
                var elem = e.srcElement||e.target;
                while(elem){
                    if(elem.id == "whatToSearch"){
                        return
                    }
                    elem = elem.parentNode;
                }
                this.isShowHomeSearchCondition = false
            },
            toggleLoginForm : function () {
                this.showForm.login = !this.showForm.login
            },
            loginFormOpen : function () {
                GlobleFun.validate("#loginForm");
                this.hideAllDialog()
                this.showForm.login = true;
            },
            login : function () {
                var self = this;
                var valid =  $("#loginForm").valid();
                if(!valid) return;

                if(self.isRememberPhone){ // 是否记住手机号
                    LS.set('loginPhone',self.loginData.mobile)
                }else{
                    LS.remove('loginPhone')
                }

                $.post({
                    url: window.YUNAPI.login,
                    data : self.loginData,
                    success: function (data ,status, xhr) {
                        console.log(data);
                        var status = data.status == 1 ? 'success' : 'error';
                        APP.$message({
                            message: data.message,
                            type: status,
                            duration : 2000
                        });
                        if(data.status == 1){
                            data.data.access_token = xhr.getResponseHeader('access-token');
                            data.data.client = xhr.getResponseHeader('client');
                            self.$store.commit('personalDataChange',data.data);//保存个人信息

                            self.showForm.login = false;
                            router.replace(self.$route.path);  // 刷新页面
                        }
                    },
                    error : function () {

                    }
                });
            },
            authLogin(){
                var self = this
                $.post({
                    url: window.YUNAPI.login,
                    data : self.authLoginData,
                    success: function (data ,status, xhr) {
                        console.log(data);
                        var status = data.status == 1 ? 'success' : 'error';
                        APP.$message({
                            message: data.message,
                            type: status,
                            duration : 2000
                        });
                        if(data.status == 1){
                            data.data.access_token = xhr.getResponseHeader('access-token');
                            data.data.client = xhr.getResponseHeader('client');
                            self.$store.commit('personalDataChange',data.data);//保存个人信息

                            self.hideAllDialog();
                            router.replace(self.$route.path);  // 刷新页面
                        }
                    },
                    error : function () {

                    }
                });
            },
            regOpen : function () {
                GlobleFun.validate("#regForm");
                this.hideAllDialog();
                this.showForm.reg = true;
            },
            submitReg : function () {
                var self = this;
                var valid =  $("#regForm").valid();
                if(!valid) return;
                self.regData.name = self.regData.surname + self.regData.username
                $.post({
                    url: window.YUNAPI.register,
                    data : self.regData,
                    success: function (data ,status, xhr) {
                        console.log(data)
                        var status = data.status == 1 ? 'success' : 'error';
                        APP.$message({
                            message: data.message,
                            type: status,
                            duration : 2000
                        });
                        if(data.status == 1){

                            data.data.access_token = xhr.getResponseHeader('access-token');
                            data.data.client = xhr.getResponseHeader('client');
                            self.$store.commit('personalDataChange',data.data);//保存个人信息

                            self.showForm.reg = false
                        }
                    },
                    error : function () {
                    }
                });
            },
            sendPhoneCode : function () {
                var self = this;
                var success = function (data) {
                    self.regData.code_token = data.data;
                };
                GlobleFun.sendPhoneCode(this.regData.mobile,success,'.sendcode')
                return false
            },
            sendChangePasswordCode : function (e) {
                var self = this;
                var success = function (data) {
                    self.changePassWordData.code_token = data.data;
                };
                GlobleFun.sendPhoneCode(this.changePassWordData.mobile,success,e.target);
                return false
            },
            sendAuthLoginPhoneCode(){
                var self = this;
                var success = function (data) {
                    self.authLoginData.code_token = data.data;
                };
                GlobleFun.sendPhoneCode(this.authLoginData.mobile,success,'#sendAuthLoginPhoneCode');
                return false
            },
            forgetPasswordFormOpen(){
                this.hideAllDialog()
                this.showForm.forgetPassword = true;
            },
            forgetPasswordClose(){
                this.changePassWordStep = 1
            },
            authLoginFormOpen(){
                this.hideAllDialog()
                this.showForm.authLogin = true

            },
            hideAllDialog(){
                for(var i in this.showForm){
                    this.showForm[i] = false
                }
            },
            changePasswordNext(){
                if(!this.changePassWordData.code_token){
                    APP.$message({
                        message: "请先获取验证码",
                        type: 'error',
                        duration : 2000
                    });
                    return
                }
                if(this.changePassWordData.auth_code.length < 6){
                    APP.$message({
                        message: "请输入正确的验证码",
                        type: 'error',
                        duration : 2000
                    });
                    return
                }
                this.changePassWordStep = 2
            },
            changePasswordNow(){
                var self = this;
                if(!this.changePassWordData.password || !this.changePassWordData.password_confirmation){
                    APP.$message({
                        message: "密码及确认密码不能为空",
                        type: 'error',
                        duration : 2000
                    });
                    return
                }

                $.ajax({
                    type :'put',
                    url: window.YUNAPI.host + 'api/auth/password',
                    data : self.changePassWordData,
                    success: function (data ,status, xhr) {

//                        console.log(data)
                        GlobleFun.httpMessage(data)

                        if(data.status == 1){
                            self.hideAllDialog()
                            GlobleFun.clearObj(self.changePassWordData)
                            self.changePassWordData.type = 'sms'
                        }
                    },
                    error : function () {
                    }
                });

            }
        }

    }
</script>
