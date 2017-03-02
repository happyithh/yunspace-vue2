<template>
    <div class="ew_back">
        <div class="ew">
            <img src="/static/images/error.png">
        </div>
        <div class="ew_word">
            <div class="ew_w">
                <span>ERROR</span><br>
                非常抱歉，您访问的页面不存在
            </div>
            <a href="javascript:" @click="back" class="ew_btn">
                返回至刚才的页面
            </a>
            <a href="" onclick="window.location.reload();"  class="ew_a">
                刷新
            </a>
            <div class="clear"></div>
        </div>
        <div class="ew_guide">
            <p class="ew_guide_left">您可以直接查看</p>
            <ul class="ew_guide_right clearfix">
                <router-link tag="li" to="/" exact>
                    <a>首页</a>
                </router-link>
                <router-link tag="li" to="/event">
                    <a>办活动</a>
                </router-link>
                <router-link tag="li" to="/openshop">
                    <a>要开店</a>
                </router-link>
                <router-link tag="li" to="/ip">
                    <a>找IP</a>
                </router-link>
                <router-link tag="li" to="/found">
                    <a>新发现</a>
                </router-link>
            </ul>
        </div>
    </div>
</template>

<script>

    import Lib from 'assets/Lib.js'
    import Owl from 'assets/owl.js'

    import 'assets/css/component.css';
    import 'assets/css/404.css';
    //  import holder from 'http://cdn.bootcss.com/holder/2.9.4/holder.js';

    //import moduleHeader from 'components/module-header';
    //import moduleFooter from 'components/module-footer';

    export default{
        data(){
            return { }
        },
        components: {

        },
        mounted(){

        },
        methods: {
            //获取活动人数、类型
            back(){
                router.back();
            }
        }

    }
</script>
