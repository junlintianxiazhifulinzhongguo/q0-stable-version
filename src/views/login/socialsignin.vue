<template>
  <div class="social-signup-container">
    <div class="sign-btn" @click="wechatHandleClick('wechat')">
      <span class="wx-svg-container"><svg-icon icon-class="wechat" class="icon"/></span> 微信
    </div>
    <div class="sign-btn" @click="tencentHandleClick('tencent')">
      <span class="qq-svg-container"><svg-icon icon-class="qq" class="icon"/></span> QQ
    </div>
    <div class="sign-btn" @click="alipayHandleClick('alipay')">
      <span class="al-svg-container"><svg-icon icon-class="alipay" class="icon"/></span> 支付宝
    </div>
  </div>
</template>

<script>
import openWindow from '@/utils/openWindow'
import { getAuthUrl } from '@/api/login'
export default {
  name: 'SocialSignin',
  data() {
    return {
      wechat: '',
      qq: '',
      alipay: '',
      thirdpart:['wechat','qq','alipay']
    }
  },
  mounted() {
    this.getAuthUrl()
  },
  methods: {
    async getAuthUrl() {
      for (let value of this.thirdpart) {
        const response = await getAuthUrl(value)
        const { data } = response
        const { auth_url } = data
        switch(value)
        {
        case 'wechat':
          this.wechat = auth_url
          break;
        case 'qq':
          this.qq = auth_url
          break;
        default:
          this.alipay = auth_url
        }
      } 
    },
    wechatHandleClick(thirdpart) {
      alert('ok')
      // this.$store.commit('SET_AUTH_TYPE', thirdpart)
      // const appid = 'xxxxx'
      // const redirect_uri = encodeURIComponent('xxx/redirect?redirect=' + window.location.origin + '/auth-redirect')
      // const url = 'https://open.weixin.qq.com/connect/qrconnect?appid=' + appid + '&redirect_uri=' + redirect_uri + '&response_type=code&scope=snsapi_login#wechat_redirect'
      // openWindow(url, thirdpart, 540, 540)
    },
    tencentHandleClick(thirdpart) {
      alert('ok')
      // this.$store.commit('SET_AUTH_TYPE', thirdpart)
      // const client_id = 'xxxxx'
      // const redirect_uri = encodeURIComponent('xxx/redirect?redirect=' + window.location.origin + '/auth-redirect')
      // const url = 'https://graph.qq.com/oauth2.0/authorize?response_type=code&client_id=' + client_id + '&redirect_uri=' + redirect_uri
      // openWindow(url, thirdpart, 540, 540)
    },
    alipayHandleClick(thirdpart) {
      this.$store.commit('SET_AUTH_TYPE', thirdpart)
      openWindow(this.alipay, thirdpart, 540, 540)
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
  .social-signup-container {
    margin: 20px 0;
    .sign-btn {
      display: inline-block;
      cursor: pointer;
    }
    .icon {
      color: #fff;
      font-size: 24px;
      margin-top: 8px;
    }
    .wx-svg-container,
    .qq-svg-container,
    .al-svg-container {
      display: inline-block;
      width: 40px;
      height: 40px;
      line-height: 40px;
      text-align: center;
      padding-top: 1px;
      border-radius: 4px;
      margin-bottom: 20px;
      margin-right: 5px;
    }
    .wx-svg-container {
      background-color: #24da70;
    }
    .qq-svg-container {
      background-color: #6BA2D6;
      margin-left: 50px;
    }
    .al-svg-container {
      background-color: rgb(24, 127, 224);
      margin-left: 50px;
    }
  }
</style>
