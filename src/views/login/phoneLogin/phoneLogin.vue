<template>
    <div class='user-login login-win'>
           <div class='title'>登录</div>
           <div class='form'>
              <div class='form-list user'>
                <div class='icon user-icon'></div>
                <input type='text' placeholder='请输入手机号' v-model="phone">
              </div>
              <div class='form-list code'>
                <input type='text' placeholder='请输入您看到的验证码' v-model="imgCode">
                <div class='img-code'><img :src="codeImg"></div>
                <div class='get-code' @click="changeImg">看不清？换一张</div>
              </div>
              <div class='form-list pwd'>
                <div>
                    <div class='icon pwd-icon'></div>
                    <input type='password' class="verificationCode" placeholder='请输入验证码' v-model="phoneCode">
                </div>
                <button class="getCode" @click="getPhoneCode" v-if="getCode">获取验证码</button>
                <button class="getCode agin" v-else>{{seconds}}秒后再次获取</button>
              </div>
              <div class='form-list login' @click="login">
                登 录
              </div>
              <div class='form-list register'>
                没有账号？
                <span class='regist' @click="regist">去注册！</span>
              </div>
              <div class='form-list other-login clear'>
                <div class='spap-login' @click="spapLogin">
                  <div class='spap-icon'></div>
                  司派授权登录
                </div>
                <div class='password-login' @click="passwordLogin">
                  <div class='password-icon'></div>
                  账号密码登陆
                </div>
              </div>
           </div>
        </div>
</template>
<script>
import Until from '../../../until/until.js'
export default {
    data(){
        return{
            imgCode:'',         //图片验证码
            codeImg:'',       //验证码的图片
            phone:'',         //电话号码
            imgCode:'',          //图片验证码
            imgId:'',           //图片验证码ID
            phoneCode:'',       //手机验证吗
            getCode:true,       //显示获取验证码
            seconds:60,       //倒计时
        }
    },
    methods:{
        checkForm(){
          let phoneCheck = Until.checkPhone(this.phone)
          if(phoneCheck != 'success'){
            this.$message({
              type:'error',
              message:'手机号无效'
            })
            return false
          }else if(this.imgCode == ''){
            this.$message({
              type:'error',
              message:'请输入图片验证码'
            })
            return false
          }else if(this.phoneCode == ''){
            this.$message({
              type:'error',
              message:'请输入手机验证码'
            })
            return false
          }else{
            return true
          }
        },
        login(){
            if(this.checkForm()){
              let data = {
                phone: this.phone,
                code: this.phoneCode,
                imgId: this.imgId,
                imgCode: this.imgCode,
              }
              this.Http.post(this.Action.phoneLogin,data).then((res) => {
                  this.$message({
                    type:'success',
                    message:'登陆成功'
                  })
                  sessionStorage.setItem('userInfo',JSON.stringify(res))
                  this.$store.commit('setUserInfo')
                  this.$router.push({path:'/'})
              }).catch((err) => {
                Until.ErrorCode(err.code);
              })
            }
        },
        spapLogin(){            //司派登陆
            this.$emit('toggleLogin',1)
        },
        passwordLogin(){               //手机号快捷登陆
            this.$emit('toggleLogin',0)
        },
        regist(){                   //注册
            this.$router.push({path:'/register'})
        },
        //获取手机验证码
        getPhoneCode(){
          let phoneCheck = Until.checkPhone(this.phone)
          if(phoneCheck != 'success'){
            this.$message({
              type:'error',
              message:'手机号无效'
            })
            return false
          }else if(this.imgCode == ''){
            this.$message({
              type:'error',
              message:'请输入图片验证码'
            })
            return false
          }
          let data = {
            phone : this.phone,
            imgId : this.imgId,
            imgCode : this.imgCode
          }
          this.Http.post(this.Action.getPhoneCode, data).then((res) => {
              this.getCode = false
              let timeInter = setInterval(() => {
                this.seconds--
                if(this.seconds <= 0){
                  this.getCode = true;
                  clearInterval(timeInter)
                }
              },1000)
          }).catch((res) => {
            Until.ErrorCode(res.code);
          })
        },
        //获取图片验证码
        getImgCode(){
         this.Http.post(this.Action.imgCode).then((res) => {
            this.codeImg = res.imgPath
            this.imgId = res.imgId
          }).catch((err) => {
            Until.ErrorCode(res.code);
          });
        },
        //换一张
        changeImg(){
          this.getImgCode()
        }
    },
    mounted(){
      this.getImgCode()
    }
}
</script>
<style lang="less" scoped>
    .login-win {
      box-sizing: border-box;
      position: absolute;
      top: 174px;
      left: 50%;
      width: 520px;
      padding-top: 42px;
      margin-left: -260px;
      background: #fff;
      color: #fff;
      .title {
        margin-bottom: 43px;
        text-align: center;
        font-size: 24px;
        color: #F58523;
        letter-spacing: 6px;
      }
      .form {
        padding-left: 50px;
        padding-right: 50px;
        > div {
          margin-bottom: 19px;
        }
        .form-list {
          width: 420px;
          height: 45px;
          margin-right: auto;
          margin-left: auto;
          background-color: #F8F9FC;
          line-height: 45px;
          border-radius: 2px;
          .icon {
            float: left;
            width: 50px;
            height: 45px;
            background-repeat: no-repeat;
            background-position: center;
            background-color: #F8F9FC;
            &.user-icon {
              background-image: url('../../../assets/login/user-icon.jpg');
            }
            &.pwd-icon {
              background-image: url('../../../assets/login/verCode.png')
            }
          }
          input {
            width: 300px;
            height: 45px;
            background-color: #F8F9FC;
            font-size: 14px;
            color: #606266;
            outline: none;
          }
          .verificationCode{
            width: 190px;
          }
          .getCode{
            background-color: #F58523;
            height: 45px;
            width: 157px;
            border: none;
            font-family: PingFang-SC-Medium;
            font-size: 14px;
            color: #FFFFFF;
            letter-spacing: 0;
            text-align: center;
            outline: none;
            cursor: pointer;
            &.agin{
              background-color: #CCCCCC;
              cursor: default;
            }
          }
        }
        .pwd{
            background: none;
            display: flex;
            justify-content: space-between;
            margin-bottom: 67px;
        }
        .login {
          background: #F58523;
          text-align: center;
          font-size: 14px;
          color: #FFFFFF;
          cursor: pointer;
        }
        .code {
          background: transparent;
          input, div {
            float: left;
            font-size: 14px;
          }
          input {
            padding-left: 20px;
            width: 180px;
            margin-right: 10px;
          }
          .img-code {
            width: 90px;
            height: 45px;
            margin-right: 10px;
            background-color: #fff;
            img{
              vertical-align: middle;
            }
          }
          .get-code {
            width: 100px;
            height: 45px;
            line-height: 45px;
            color: #26242A;
            cursor: pointer;
          }
        }
        .register {
          height: 20px;
          line-height: 20px;
          margin-bottom: 48px;
          background: transparent;
          font-size: 14px;
          color: #26242A;
          .regist{
            color: #4393F9;
            cursor: pointer;
          }
        }
        .other-login {
          background: transparent;
          > div {
            float: left;
            box-sizing: border-box;
            width: 186px;
            height: 42px;
            border-radius: 100px;
            line-height: 42px;
            font-size: 14px;
            cursor: pointer;
            > div {
              float: left;
              width: 50px;
              height: 42px;
              background-repeat: no-repeat;
              background-position: center;
            }
          }
          .spap-login {
            border: 1px solid #4393F9;
            margin-right: 40px;
            color: #4393F9;
            .spap-icon {
              background-image: url('../../../assets/login/spap.png');
            }
          }
          .password-login {
            border: 1px solid #F58523;
            color: #F58523;
            letter-spacing: 2px;
            .password-icon {
              background-image: url('../../../assets/login/pwd.png');
            }
          }
        }
      }
    }
</style>
