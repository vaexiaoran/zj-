<template>
  <div id="userLayout" :class="['user-layout-wrapper', device]">
    <div class="container">
      <carousel></carousel>
      <div class="top">
        <!--<div class="header">-->
        <!--<a href="/">-->
        <img src="../../assets/zjimg/logo.png" class="logozj">
        <div class="setPage">
          <a href="javascript:;" @click="SetHome(this,'http://localhost:3000/user/login')">设为首页</a> |
          <a href="javascript:;" @click="AddFavorite('智能后台管理系统','http://localhost:3000/user/login')">加入收藏</a>


        </div>
        <div style="clear: both;"></div>
        <!--<span class="title">Centrin Boot</span>-->
        <!--</a>-->
        <!--</div>-->
        <!--<div class="desc">-->
        <!--Centrin-Ecloud 是中国领先的出版物信息与数据技术服务商-->
        <!--</div>-->
      </div>

      <route-view></route-view>

      <div class="footer">
        <div class="links">
          <a href="http://doc.jeecg.com" target="_blank">关于中金易云</a>|
          <a href="https://github.com/zhangdaiscott/jeecg-boot" target="_blank">联系我们</a>|
          <a href="https://github.com/zhangdaiscott/jeecg-boot/blob/master/LICENSE" target="_blank">© Copyright
            2018-2020 中金易云科技有限责任公司</a>
        </div>
        <!--<div class="copyright">-->
        <!---->
        <!--© Copyright 2018-2020 <a href="http://www.jeecg.com" target="_blank">中金易云科技有限责任公司</a> -->
        <!--</div>-->
      </div>
    </div>
  </div>
</template>

<script type="text/javascript">
  import RouteView from '@/components/layouts/RouteView'
  import { mixinDevice } from '@/utils/mixin.js'
  import carousel from '@/components/public/carousel'


  export default {
    name: 'UserLayout',
    components: { RouteView, carousel },
    mixins: [mixinDevice],
    data() {
      return {}
    },
    mounted() {
      document.body.classList.add('userLayout')
    },
    methods: {
      //加入收藏
      AddFavorite(title, url) {
        try {
          window.external.addFavorite(url, title);
        }
        catch (e) {
          try {
            window.sidebar.addPanel(title, url, "");
          }
          catch (e) {


            this.$notification.open({
              message: '智慧书城提醒您',
              description:
                '抱歉，您所使用的浏览器无法完成此操作。加入收藏失败，请使用Ctrl+D进行添加',

              icon: <a-icon type="smile" style="color: #108ee9" />

            });
           // alert("抱歉，您所使用的浏览器无法完成此操作。\n\n加入收藏失败，请使用Ctrl+D进行添加");
          }
        }
      },
      //设为首页
      SetHome(obj,url) {
        try{
          obj.style.behavior='url(#default#homepage)';
          obj.setHomePage(url);
        }catch(e){
          if(window.netscape){
            try{
              netscape.security.PrivilegeManager.enablePrivilege("UniversalXPConnect");
            }catch(e){
             // alert("抱歉，此操作被浏览器拒绝！\n\n请在浏览器地址栏输入“about:config”并回车然后将[signed.applets.codebase_principal_support]设置为'true'");
              this.$notification.open({
                message: '智慧书城提醒您',
                description:
                  '抱歉，此操作被浏览器拒绝！请在浏览器地址栏输入“about:config”并回车然后将[signed.applets.codebase_principal_support]设置为"true"',
                icon: <a-icon type="smile" style="color: #108ee9" />,
                onClick: () => {
                  console.log('Notification Clicked!');
                },
              });
            }
          }else{
            //alert("抱歉，您所使用的浏览器无法完成此操作。\n\n您需要手动将【"+url+"】设置为首页。");
            this.$notification.open({
              message: '智慧书城提醒您',
              description:
                '抱歉，您所使用的浏览器无法完成此操作。您需要手动将其设置为首页。',
              icon: <a-icon type="smile" style="color: #108ee9" />,
              onClick: () => {
                console.log('Notification Clicked!');
              },
            });
          }
        }








      }


    },
    beforeDestroy() {
      document.body.classList.remove('userLayout')
    }
  }
</script>


<style lang="less" scoped>
  #userLayout.user-layout-wrapper {
    height: 100%;
    overflow: hidden;
    &.mobile {
      .container {
        .main {
          max-width: 368px;
          width: 98%;
        }
      }
    }

    .container {
      box-sizing: border-box;
      width: 100%;
      height: 100%;
      //background: #f0f2f5 url(~@/assets/background.svg) no-repeat 50%;
      background-size: 100%;
      //padding: 110px 0 144px;
      position: relative;

      a {
        text-decoration: none;
      }

      /*.top {*/
      /*text-align: center;*/

      /*.header {*/
      /*height: 44px;*/
      /*line-height: 44px;*/

      /*.badge {*/
      /*position: absolute;*/
      /*display: inline-block;*/
      /*line-height: 1;*/
      /*vertical-align: middle;*/
      /*margin-left: -12px;*/
      /*margin-top: -10px;*/
      /*opacity: 0.8;*/
      /*}*/

      /*.logo {*/
      /*height: 42px;*/
      /*vertical-align: top;*/
      /*margin-right: 16px;*/
      /*border-style: none;*/
      /*}*/

      /*.title {*/
      /*font-size: 33px;*/
      /*color: rgba(0, 0, 0, .85);*/
      /*font-family: "Chinese Quote", -apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", "Helvetica Neue", Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";*/
      /*font-weight: 600;*/
      /*position: relative;*/
      /*top: 2px;*/
      /*}*/
      /*}*/
      /*.desc {*/
      /*font-size: 14px;*/
      /*color: rgba(0, 0, 0, 0.45);*/
      /*margin-top: 12px;*/
      /*margin-bottom: 40px;*/
      /*}*/
      /*}*/

      .main {

        /*margin: 0 auto;*/
        margin-left: 70%;
        // margin-top:5%;
        border-radius: 10px;
      }
      .top {
        width: 100%;
        height: 50px;
        box-sizing: border-box;
        background: #fff;
        z-index: 10;
        padding: 0 70px;

      }
      .logozj {
        width: 140px;
        height: 30px;
        display: inline-block;
        margin-top: 10px;
        float: left;
      }
      .setPage {
        float: right;
        line-height: 50px;
      }
      .setPage a {
        color: #888;
        font-size: 12px;
      }
      .setPage a:nth-of-type(1) {
        padding-right: 10px;
      }
      .setPage a:nth-of-type(2) {
        padding-left: 10px;
      }

      .footer {
        position: absolute;
        width: 100%;
        height: 60px;
        // padding: 0 16px;
        // margin: 48px 0 24px;
        text-align: center;
        background: #fff;
        bottom: 0px;
        border-top: 1px solid #e5e5e5;
        line-height: 67px;
        .links {
          margin-bottom: 8px;
          font-size: 14px;
          a {
            color: #888;
            transition: all 0.3s;
            font-size: 12px;
            /*&:not(:last-child) {*/
            /*padding-right: 10px;*/
            /*}*/
            &:nth-of-type(1) {
              padding-right: 10px;
            }
            &:nth-of-type(2) {
              padding-left: 10px;
              padding-right: 10px;
            }
            &:nth-of-type(3) {
              padding-left: 10px;
            }
          }
        }

      }
    }
  }
</style>