<template>
  <div class='search-con'>
    <div class='search-par' :data-id='list.id' :data-type='list.type'>
      <div class='search-people clear w1180'>
        <div class='img'>
          <a href='javascript:;' @click='openCompanyDetail(list.id, list.type)'><img :src='list.businessLicense' /></a>
        </div>
        <div class='desc'>
          <div class='tit'>
              <a href='javascript:;' @click='openCompanyDetail(list.id, list.type)'>{{list.name}}</a>
              <a href='javascript:;' class='operator' @click='makeSure' v-if='list.claimState == 1'>未认证</a>
              <span class='operator' v-else-if='list.claimState == 2'>审核中</span>
              <span class='operator' v-else-if='list.claimState == 3'>已认证</span>
          </div>
          <div class='con'>
            <div class='list'>
              企业证书: {{list.creditCode}}
            </div>
            <div class='list'>
              通讯地址: {{list.address}}
            </div>
          </div>
        </div>
        <div class='jc-list credit'>
          <div class='num'>{{list.rating}}</div>
          <div class='icon-txt'>信用等级</div>
        </div>
        <div class='jc-list honor'>
          <div class='num'>{{list.commendCount}}</div>
          <div class='icon-txt'>荣誉</div>
        </div>
        <div class='jc-list no-honor'>
          <div class='num'>{{list.loseCreditCount}}</div>
          <div class='icon-txt'>失信信息</div>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
import Until from '../../until/until.js'

  export default {
    name: 'searchCompany',

    props: ['list'],

    components: {

    },

    methods: {
      openCompanyDetail(id, type) {
        this.$router.push({
          path: '/credit/company',
          query: {id, type}
        });
      },

      makeSure() {
        if(Until.getUserToken()) {
          if(Until.getUser().user.claimState != 1) {
            this.$message.error("您已认证过，请勿重复认领");
            return;
          }else {
            this.$router.push({
              path: '/personal'
            });
          }
        }else {
          this.$message.error("请您先去登录");
        }
      }
    }
  }
</script>

<style lang='less' scoped>
  .search-par {
    .search-people {
        box-sizing: border-box;
        height: 246px;
        border: 1px solid #DCDFE6;
        padding-top: 23px;
        padding-bottom: 23px;
        padding-left: 20px;
        padding-right: 33px;
        margin-bottom: 10px;
        > div {
          float: left;
          color: #4A4A4A;
        }
        .img {
          margin-right: 22px;
          width: 135px;
          height: 199px;
        }
        .desc {
          width: 264px;
          margin-right: 153px;
          .tit {
            margin-bottom: 20px;
            font-size: 24px;
            a {
              color: #4a4a4a;
              font-weight: bold;
            }
            .operator {
              padding-left: 15px;
              height: 15px;
              line-height: 15px;
              background-image: url('../../assets/search/wrl.png');
              background-repeat: no-repeat;
              background-position: left top;
              font-size: 14px;
              color: #F58523;
              &.received {
                background-image: url('../../assets/search/rl.png');
              }
            }
          }
          .list {
            height: 22px;
            line-height: 22px;
            font-size: 14px;
            span {
              a {
                color: #4393F9;
              }
            }
          }
        }
        .jc-list {
          float: left;
          margin-right: 120px;
          .num {
            height: 98px;
            line-height: 98px;
            margin-top: 33px;
            text-align: center;
            font-size: 86px;
          }
          .icon-txt {
            height: 25px;
            line-height: 25px;
            background-repeat: no-repeat;
            background-position: left center;
            font-size: 16px;
            color: #9B9B9B;
          }
            &.credit {
             .num {

             }
             .icon-txt {
               padding-left: 30px;
               background-image: url('../../assets/search/credit.png');
             }
            }
            &.honor {
             .num {

             }
             .icon-txt {
               padding-left: 33px;
               background-image: url('../../assets/search/honor.png');
             }
           }
           &.no-honor {
            margin-right: 0;
            .num {

            }
            .icon-txt {
              padding-left: 28px;
              background-image: url('../../assets/search/no-honor.png');
            }
          }
        }
      }
  }

</style>
