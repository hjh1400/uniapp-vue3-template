<template>
  <view class="page-wrap">
    <u-navbar title="" placeholder left-icon="" right-icon="camera-fill" />
    <view class="flex items-center bg-white pb-30rpx pl-30rpx pr-20rpx">
      <view class="mr-10rpx">
        <u-avatar :src="userImgDefault" size="70" />
      </view>
      <view class="flex-1" @click="toUserInfo">
        <view v-if="userCodeView" class="pb-20rpx font-size-30rpx">
          <view>{{userCode}}</view>
        </view>
        <view v-else="userCodeView" class="pb-20rpx font-size-30rpx">
          <view>微信用户</view>
        </view>
      </view>
      <view class="ml-40rpx p-40rpx" v-if="!userCodeView">
        <u-button type="error" shape="circle" size="mini" @tap="getUserProfiles">点击登陆</u-button>
      </view>
      <view class="ml-10rpx p-10rpx">
        <u-icon name="arrow-right" color="#969799" />
      </view>
    </view>

    <view class="mt-20rpx bg-white">
      <u-cell-group>
        <u-cell icon="order" title="我的预约" is-link @click="toyy()" />
      </u-cell-group>
    </view>

    <view class="mt-20rpx bg-white">
      <u-cell-group>
        <u-cell icon="setting" title="设置" is-link />
      </u-cell-group>
    </view>
  </view>
</template>

<script>
 export default {
   name: 'user',
   data() {
     return {
       "userCodeView":false,
       "userCode":"微信用户",
       "userImgDefault":"https://mmbiz.qpic.cn/mmbiz/icTdbqWNOwNRna42FI242Lcia07jQodd2FJGIYQfG0LAJGFxM4FbnQP6yfMxBgJ0F3YRqJCJ1aPAK2dQagdusBZg/0",
       "userInfo":null
     };
   },methods:{
     toUserInfo(){
       if(this.userCodeView){
         //登陆跳转个人信息
          console.log(this.userCodeView);
       }else{
         //跳转登陆页面
          uni.navigateTo({
            url:"/pages/common/login/index"
          })
       }
     },
     getUserProfiles(e) {
         // 推荐使用wx.getUserProfile获取用户信息，开发者每次通过该接口获取用户个人信息均需用户确认
         // 开发者妥善保管用户快速填写的头像昵称，避免重复弹窗
         uni.getUserProfile({
           desc: '用于完善会员资料', // 声明获取用户个人信息后的用途，后续会展示在弹窗中，请谨慎填写
           success: (res) => {
             this.userImgDefault=res.userInfo.avatarUrl;
             this.userCode=res.userInfo.nickName;
             this.userCodeView=true;
             uni.setStorage({
               key:"userinfo",
               data:JSON.stringify(res.userInfo)
             })
             console.log(res.userInfo);
           }
         })
       },
       toyy(){
         this.checkUser();
         //
         //跳转预约页面
         uni.navigateTo({
           url:"/pages/common/login/index"
         })
       },
       checkUser(){
         if(!this.userCodeView){
           //未登陆 跳转登陆
          console.log("为登陆");
           this.getUserProfiles();
         }
       }
   }
 };
</script>
