<template>
  <div>
    <div class='bg'>
        <div class='bg-par w1180 clear'>
          <Register @toggleLogin='toggleLogin'></Register>
        </div>
    </div>
  </div>

</template>

<script>
import Register from './component/component'
  export default {
    name: 'regist',
    components: {
      Register
    },
    data(){
      return{
      }
    },
    methods: {
      toggleLogin(num){
        this.loginNum = num;
        console.log('0111')
      }
    },
    mounted(){
    }
  }
</script>

<style lang='less' scoped>
  .bg {
    position: relative;
    width: 100%;
    height: 1080px;
    background-image: url('../../assets/login/bg.png');
    background-repeat: no-repeat;
    overflow: hidden;
    .bg-par {
      height: 100%;
      img {
        display: block;
      }
    }

    // .login-win {
    //   box-sizing: border-box;
    //   position: absolute;
    //   top: 174px;
    //   left: 50%;
    //   width: 520px;
    //   height: 520px;
    //   padding-top: 42px;
    //   margin-left: -260px;
    //   background: #fff;
    //   color: #fff;
    //   .title {
    //     margin-bottom: 43px;
    //     text-align: center;
    //     font-size: 24px;
    //     color: #F58523;
    //   }
    //   .form {
    //     padding-left: 50px;
    //     padding-right: 50px;
    //     > div {
    //       margin-bottom: 19px;
    //     }
    //     .form-list {
    //       width: 420px;
    //       height: 45px;
    //       margin-right: auto;
    //       margin-left: auto;
    //       background-color: #F8F9FC;
    //       line-height: 45px;
    //       border-radius: 2px;
    //       .icon {
    //         float: left;
    //         width: 50px;
    //         height: 45px;
    //         background-repeat: no-repeat;
    //         background-position: center;
    //         &.user-icon {
    //           background-image: url('../../assets/login/user-icon.jpg');
    //         }
    //         &.pwd-icon {
    //           background-image: url('../../assets/login/pwd-icon.jpg')
    //         }
    //       }
    //       input {
    //         width: 300px;
    //         height: 45px;
    //         background-color: #F8F9FC;
    //         font-size: 14px;
    //         color: #CCCCCC;
    //         outline: none;
    //       }
    //     }
    //     .user {

    //     }
    //     .pwd {
    //       .pwd-eye-icon {
    //         float: right;
    //         width: 50px;
    //         height: 45px;
    //         background-repeat: no-repeat;
    //         background-position: center;
    //         background-image: url('../../assets/login/eye.png');
    //         cursor: pointer;
    //         &.open {
    //           background-image: url('../../assets/login/eye-open.png');
    //         }
    //       }
    //     }
    //     .login {
    //       background: #F58523;
    //       text-align: center;
    //       font-size: 14px;
    //       color: #FFFFFF;
    //       cursor: pointer;
    //     }
    //     .code {
    //       background: transparent;
    //       input, div {
    //         float: left;
    //         font-size: 14px;
    //       }
    //       input {
    //         padding-left: 20px;
    //         width: 180px;
    //         margin-right: 10px;
    //       }
    //       .img-code {
    //         width: 90px;
    //         margin-right: 10px;
    //         background-color: #F8F9FC;
    //       }
    //       .get-code {
    //         width: 100px;
    //         height: 45px;
    //         line-height: 45px;
    //         color: #26242A;
    //         cursor: pointer;
    //       }
    //     }
    //     .register {
    //       height: 20px;
    //       line-height: 20px;
    //       margin-bottom: 48px;
    //       background: transparent;
    //       font-size: 14px;
    //       color: #26242A;
    //       .register-btn {
    //         color: #4393F9;
    //       }
    //     }
    //     .other-login {
    //       background: transparent;
    //       > div {
    //         float: left;
    //         box-sizing: border-box;
    //         width: 186px;
    //         height: 42px;
    //         border-radius: 100px;
    //         line-height: 42px;
    //         font-size: 14px;
    //         cursor: pointer;
    //         > div {
    //           float: left;
    //           width: 50px;
    //           height: 42px;
    //           background-repeat: no-repeat;
    //           background-position: center;
    //         }
    //       }
    //       .spap-login {
    //         border: 1px solid #4393F9;
    //         margin-right: 40px;
    //         color: #4393F9;
    //         .spap-icon {
    //           background-image: url('../../assets/login/spap.png');
    //         }
    //       }
    //       .phone-login {
    //         border: 1px solid #F58523;
    //         color: #F58523;
    //         .phone-icon {
    //           background-image: url('../../assets/login/phone.png');
    //         }
    //       }
    //     }
    //   }
    // }
  }
</style>
