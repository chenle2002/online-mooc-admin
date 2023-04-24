<template>
  <div class="video-study">
    <header>
      <div class="banner">
        <div class="back"><i class="iconfont iconheiyemoshi-fanhui"></i>返回学堂</div>
        <div class="source-con"><p class="source-name">{{dataList.name}}</p>
          <p class="source-down"><span class="source-n"></span><span>联盟推荐</span></p></div>
        <div class="header_userInfo"><a href="https://onlineh5.zhihuishu.com/onlineWeb.html#/entry" target="_blank"
                                        class="fl"><span class="userInfo_header"><img width="32" height="32"
                                                                                      src="https://image.zhihuishu.com/zhs/ablecommons/demo/201804/5e314c660d31448d94fc201d434ca736.jpg"></span></a>
          <div class="userLinks">
            <ul>
              <li><a href="//user.zhihuishu.com/zhsuser/account/new" target="_self" class="userLinks_item clearfix"><em
                class="fl iconfont iconheiyemoshi-zhanghaoshezhi"></em><span class="fl">账号设置</span></a></li>
              <li><span target="_self" class="userLinks_item clearfix"><em
                class="fl iconfont iconheiyemoshi-anquantuichu"></em><span class="fl">安全退出</span></span></li>
            </ul>
          </div>
        </div>
        <div class="menudivright-r-div">
          <div class="Patternbtn-div">
            <svg aria-hidden="true" class="icon">
              <use xlink:href="#iconbaizhoumoshi"></use>
            </svg>
            <p>白昼模式</p><!----></div>
          <div class="morebtn-div showMore"><em class="iconfont iconbaizhoumoshi-gengduo"></em>
            <p>更多</p>
            <div class="Retirebtn-div"><em class="fl iconfont iconbaizhoumoshi-tuike"></em><span class="fl">退课</span>
            </div>
          </div>
          <div class="fl InformationCenter-div"><a target="_blank" href="https://onlineh5.zhihuishu.com/onlineWeb.html#/student/noticeCenter?noticeType=0">消息中心</a>
            <!----></div>
        </div>
      </div>
    </header>
    <div class="box-content">
      <div class="box-right">
        <div class="topicTitle clearfix">
          <ul>
            <li tid="1" class="tabTitle select"><span>目录</span></li>
          </ul>
        </div>
        <div class="el-scrollbar" style="height: 494px">
          <div
            class="el-scrollbar__wrap"
            style="margin-bottom: -17px; margin-right: -17px">
            <div class="el-scrollbar__view">
              <ul class="list" v-for="(item,i) in dataList">
                <span class="position_first_bg"></span>
                <li class="clearfix font_gray_inclined chapter">
                  <span :title="i" class="catalogue_title3 fl"><b>第{{ i + 1 }}章</b></span><em
                  class="chapter-em fl"></em>
                  <span class="time_ico_box fl"></span>
                  <span
                    :title="item.name"
                    class="catalogue_title fl catalogue_titleweight">{{ item.name }}
              </span>
                </li>
                <div v-for="(chapter,n) in item.children">
                  <li class="clearfix video current_play">
                        <span class="catalogue_title3 fl cataloguediv-l">
                          <b class="pl5 hour">{{ i + 1 }}.{{ n + 1 }}</b>
                        </span>
                    <div class="fl cataloguediv-c">
                          <span
                            :title="chapter.name"
                            class="catalogue_title">
                            {{ chapter.name }}
                          </span>
                      <div>
                        <b class="time_ico_half fl"></b>
                        <b class="fl time_icofinish"></b>
                        <span class="time fl">视频长度未知</span>
                      </div>
                    </div>

                  <li title="点击测试" class="chapter-test">
                      <span class="name">
                        测试功能暂不可用
                        <span>
                          <b class="finish"></b>
                        </span></span>
                    <em class="Sectionmark-em"></em>
                  </li>
                </div>
              </ul>

            </div>
          </div>
        </div>
      </div>
    </div>

  </div>

</template>
<script>
export default {
  name: "mooc",
  data() {
    return {
      dataList: [],
      name: '',
      dataListLoading: false,
      addOrUpdateVisible: false
    };
  },
  mounted() {
    // 获取数据列表
    this.dataListLoading = true;
    this.$http({
      url: this.$http.adornUrl("/course/coursetree/list/tree"),
      method: "get"
    }).then(({data}) => {
      this.dataList = data.page[0].children;
      this.name = data.page[0].name
      console.log(this.dataList, 111)
    });
  }
};
</script>

<style lang="scss" scoped>
.pdf-tab {
  display: flex;
}

.pdf-page {
  text-align: right;
}

.el-header {
  height: 60px;
  color: #3d4059;
  background: #3d84ff;
  box-shadow: 0 2px 8px 0 rgba(0, 0, 0, .1);
  z-index: 30;
  position: fixed;
  width: 100%;
  padding: 0 62px;
  left: 0
}

.el-header .banner {
  margin: 0 auto;
  min-width: 1200px;
  height: 60px;
  position: relative
}

.el-header .banner .back {
  color: #fff;
  text-decoration: none;
  font-size: 14px;
  line-height: 60px;
  opacity: .75;
  display: inline;
  cursor: pointer
}

.el-header .banner .back:hover {
  opacity: .5
}

.el-header .banner .back:hover i {
  opacity: .75
}

.el-header .banner .back i {
  font-size: 19px;
  color: #fff;
  float: left;
  margin-top: 1px;
  margin-right: 3px
}

.el-header .banner .source-con {
  position: absolute;
  left: 50%;
  text-align: center;
  top: 0;
  transform: translateX(-50%);
  -webkit-transform: translateX(-50%);
  -moz-transform: translateX(-50%);
  -ms-transform: translateX(-50%);
  -o-transform: translateX(-50%);
  margin-top: 10px
}

.el-header .banner .source-con .source-name {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  width: 300px;
  color: #fff;
  font-size: 14px
}

.el-header .banner .source-con .source-down {
  margin-top: 5px;
  display: inline
}

.el-header .banner .source-con .source-down span {
  font-size: 12px;
  color: #fff;
  opacity: .75
}

.el-header .banner .source-con .source-down .source-n {
  margin-right: 10px
}

.el-header .banner .header_userInfo {
  float: right;
  margin: 10px 0 0 30px;
  height: 26px;
  border-radius: 2px;
  line-height: 26px;
  width: 36px;
  position: relative;
  cursor: pointer;
  z-index: 51;
  padding-bottom: 24px
}

.el-header .banner .header_userInfo .userInfo_header {
  float: left;
  margin: 2px;
  height: 32px;
  width: 32px
}

.el-header .banner .header_userInfo .userInfo_header img {
  vertical-align: top;
  border-radius: 100px
}

.el-header .banner .header_userInfo:hover .userLinks {
  display: block
}

.el-header .banner .header_userInfo .userLinks {
  position: absolute;
  z-index: 51;
  display: none;
  width: 120px;
  top: 49px;
  right: 0;
  height: 80px;
  padding: 10px 0;
  background: #fff;
  box-shadow: 0 5px 15px 0 rgba(0, 0, 0, .1);
  border-radius: 2px
}

.el-header .banner .header_userInfo .userLinks li {
  height: 40px;
  line-height: 40px
}

.el-header .banner .header_userInfo .userLinks li:hover {
  background: #ededed
}

.el-header .banner .header_userInfo .userLinks li .userLinks_item {
  font-size: 13px;
  color: #2a2a2a;
  padding: 0 15px;
  display: inline-block
}

.el-header .banner .header_userInfo .userLinks li .userLinks_item .iconfont {
  margin-right: 5px;
  display: inline-block;
  color: #777
}

.el-header .banner .menudivright-r-div {
  float: right
}

.el-header .banner .menudivright-r-div .Patternbtn-div {
  float: left;
  width: 80px;
  text-align: center;
  padding-top: 8px;
  cursor: pointer;
  height: 60px;
  box-sizing: border-box
}

.el-header .banner .menudivright-r-div .Patternbtn-div:hover {
  background: #2b70e6
}

.el-header .banner .menudivright-r-div .Patternbtn-div em {
  font-size: 26px;
  display: inline-block;
  color: #cee0ff
}

.el-header .banner .menudivright-r-div .Patternbtn-div .icon {
  width: 25px;
  height: 25px
}

.el-header .banner .menudivright-r-div .Patternbtn-div p {
  font-size: 12px;
  color: #cee0ff
}

.el-header .banner .menudivright-r-div .morebtn-div {
  width: 80px;
  height: 60px;
  text-align: center;
  position: relative;
  cursor: pointer;
  float: left;
  padding-top: 8px;
  box-sizing: border-box
}

.el-header .banner .menudivright-r-div .morebtn-div:hover {
  background: #2b70e6
}

.el-header .banner .menudivright-r-div .morebtn-div em {
  font-size: 26px;
  display: inline-block;
  color: #cee0ff;
  margin-left: -3px
}

.el-header .banner .menudivright-r-div .morebtn-div p {
  font-size: 12px;
  color: #cee0ff
}

.el-header .banner .menudivright-r-div .morebtn-div:hover .Retirebtn-div {
  display: block
}

.el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div {
  display: none;
  width: 120px;
  height: 40px;
  position: absolute;
  top: 60px;
  left: 0;
  background: #fff;
  line-height: 40px;
  box-shadow: 0 5px 15px 0 rgba(0, 0, 0, .1)
}

.el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div .iconbaizhoumoshi-tuike {
  margin: 3px 0 0 12px;
  display: inline-block;
  color: #d8d8d8;
  width: 25px
}

.el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div span {
  font-size: 13px;
  color: #bfbfbf
}

.el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div:hover span {
  color: #2a2a2a
}

.el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div:hover .iconbaizhoumoshi-tuike {
  color: #bfbfbf
}

.el-header .banner .menudivright-r-div .InformationCenter-div {
  margin-left: 76px;
  margin-right: 30px;
  position: relative
}

.el-header .banner .menudivright-r-div .InformationCenter-div a {
  line-height: 60px;
  font-size: 14px;
  color: #fff;
  opacity: .75;
  cursor: pointer
}

.el-header .banner .menudivright-r-div .InformationCenter-div a:hover {
  opacity: .5
}

.el-header .banner .menudivright-r-div .InformationCenter-div .noticeTips {
  display: inline-block;
  min-width: 18px;
  height: 18px;
  background: #ff8013;
  border-radius: 50%;
  margin-left: 5px;
  color: #fff;
  line-height: 18px;
  text-align: center;
  font-size: 12px;
  position: absolute;
  top: 21px;
  right: -22px
}

.el-header .banner .menudivright-r-div .backold-div {
  font-size: 14px;
  color: #fff;
  opacity: .75;
  cursor: pointer;
  line-height: 60px
}

.el-header .banner .menudivright-r-div .backold-div:hover {
  opacity: .5
}

.el-header .banner .message-reddot {
  text-decoration: none;
  position: absolute;
  top: -6px;
  right: -14px;
  min-width: 14px;
  height: 14px;
  text-align: center;
  line-height: 14px;
  font-size: 12px;
  color: #fff;
  border-radius: 14px;
  background: #e10e01;
  padding: 0 3px !important
}

.dialog-quit .el-dialog {
  width: 400px;
  height: 480px;
  border-radius: 2px
}

.dialog-quit .el-dialog .el-dialog__header {
  padding: 20px 30px;
  padding-bottom: 15px;
  border-bottom: 1px solid #ededed
}

.dialog-quit .el-dialog .el-dialog__title {
  font-weight: 700
}

.dialog-quit .el-dialog .el-dialog__headerbtn {
  right: 30px
}

.dialog-quit .el-dialog .el-dialog__close {
  color: #777;
  font-size: 18px
}

.dialog-quit .el-dialog .el-dialog__body {
  padding: 0
}

.dialog-quit .el-dialog .el-dialog__body .quit-con {
  margin-top: 30px;
  padding: 0 30px
}

.dialog-quit .el-dialog .el-dialog__body .quit-con h2 {
  font-size: 18px;
  color: #2a2a2a;
  margin-bottom: 90px;
  line-height: 30px
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode {
  margin-bottom: 100px
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode p {
  font-size: 14px;
  color: #2a2a2a;
  letter-spacing: .25px;
  line-height: 24px;
  margin-bottom: 10px
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text {
  overflow: hidden;
  clear: both
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text .el-input {
  width: 180px;
  float: left
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text .el-input .el-input__inner {
  width: 180px;
  height: 32px;
  line-height: 32px;
  padding-left: 5px;
  box-sizing: border-box;
  background: #f6f6f6;
  border: 1px solid #ededed;
  border-radius: 2px;
  color: #2a2a2a
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text .el-input .el-input__inner:focus {
  box-shadow: inherit
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text .el-input .el-input__inner::-webkit-input-placeholder {
  font-size: 14px;
  color: #bfbfbf;
  font-weight: 100
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text .el-input .el-input__inner:-moz-placeholder, .dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text .el-input .el-input__inner::-moz-placeholder {
  font-size: 14px;
  color: #bfbfbf;
  font-weight: 100
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text .el-input .el-input__inner:-ms-input-placeholder {
  font-size: 14px;
  color: #bfbfbf;
  font-weight: 100
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text .s-canvas, .dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text img {
  margin: 0 10px;
  height: 32px;
  width: 80px;
  float: left
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text span {
  float: left;
  line-height: 32px;
  color: #777;
  font-size: 14px;
  cursor: pointer
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .error-code {
  color: #ff2a24;
  line-height: 24px;
  margin-top: 10px
}

.dialog-quit .el-dialog .el-dialog__body .con-up {
  margin-bottom: 30px
}

.dialog-quit .el-dialog .el-dialog__body .tit {
  font-size: 14px;
  color: #777;
  line-height: 24px;
  margin-bottom: 5px
}

.dialog-quit .el-dialog .el-dialog__body .con {
  font-size: 14px;
  color: #2a2a2a;
  line-height: 24px;
  font-weight: 700
}

.dialog-quit .el-dialog .el-dialog__body textarea {
  margin-bottom: 10px;
  resize: none;
  width: 340px;
  height: 80px;
  padding: 5px 10px;
  box-sizing: border-box;
  background: #f6f6f6;
  border: 1px solid #ededed;
  box-shadow: inset 0 -1px 0 0 #ededed;
  border-radius: 2px;
  color: #2a2a2a
}

.dialog-quit .el-dialog .el-dialog__body textarea::-webkit-input-placeholder {
  font-size: 14px;
  color: #bfbfbf;
  font-weight: 100
}

.dialog-quit .el-dialog .el-dialog__body textarea:-moz-placeholder, .dialog-quit .el-dialog .el-dialog__body textarea::-moz-placeholder {
  font-size: 14px;
  color: #bfbfbf;
  font-weight: 100
}

.dialog-quit .el-dialog .el-dialog__body textarea:-ms-input-placeholder {
  font-size: 14px;
  color: #bfbfbf;
  font-weight: 100
}

.dialog-quit .el-dialog .el-dialog__body .tip {
  font-size: 12px;
  color: #777;
  line-height: 18px
}

.dialog-quit .el-dialog .el-dialog__footer {
  padding: 0;
  text-align: center;
  position: absolute;
  bottom: 20px;
  left: 75px
}

.dialog-quit .el-dialog .el-dialog__footer .btn {
  background: #3d84ff;
  width: 120px;
  height: 40px;
  text-align: center;
  color: #fff;
  border: 1px solid #3d84ff;
  border-radius: 0
}

.dialog-quit .el-dialog .el-dialog__footer .btn:hover {
  background: rgba(61, 132, 255, .8)
}

.dialog-quit .el-dialog .el-dialog__footer .cancel {
  background: #fff;
  border: 1px solid #ededed;
  color: #2a2a2a
}

.dialog-quit .el-dialog .el-dialog__footer .cancel:hover {
  background: #ededed
}

.black .el-header {
  background: #2a2a2a
}

.black .el-header .banner .back {
  color: #777;
  opacity: inherit
}

.black .el-header .banner .back:hover, .black .el-header .banner .back:hover i {
  color: #bfbfbf;
  opacity: inherit
}

.black .el-header .banner .back i {
  color: #777
}

.black .el-header .banner .source-con .source-name {
  color: #bfbfbf
}

.black .el-header .banner .source-con .source-down span {
  color: #777;
  opacity: inherit
}

.black .el-header .banner .header_userInfo .userLinks {
  background: #2a2a2a;
  box-shadow: 0 5px 15px 0 rgba(0, 0, 0, .1)
}

.black .el-header .banner .header_userInfo .userLinks li:hover {
  background: #3f3f3f
}

.black .el-header .banner .header_userInfo .userLinks li .userLinks_item {
  color: #777
}

.black .el-header .banner .header_userInfo .userLinks li .userLinks_item:hover, .black .el-header .banner .header_userInfo .userLinks li .userLinks_item:hover .iconfont {
  color: #bfbfbf
}

.black .el-header .banner .menudivright-r-div .Patternbtn-div:hover {
  background: #1d1d1d
}

.black .el-header .banner .menudivright-r-div .Patternbtn-div em, .black .el-header .banner .menudivright-r-div .Patternbtn-div p {
  color: #777
}

.black .el-header .banner .menudivright-r-div .morebtn-div:hover {
  background: #1d1d1d
}

.black .el-header .banner .menudivright-r-div .morebtn-div em, .black .el-header .banner .menudivright-r-div .morebtn-div p {
  color: #777
}

.black .el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div {
  background: #2a2a2a;
  box-shadow: 0 5px 15px 0 rgba(0, 0, 0, .1)
}

.black .el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div .iconbaizhoumoshi-tuike, .black .el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div span {
  color: #3f3f3f
}

.black .el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div:hover .iconbaizhoumoshi-tuike, .black .el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div:hover span {
  color: #bfbfbf
}

.black .el-header .banner .menudivright-r-div .InformationCenter-div a {
  color: #777;
  opacity: inherit
}

.black .el-header .banner .menudivright-r-div .InformationCenter-div a:hover {
  opacity: inherit;
  color: #bfbfbf
}

.black .el-header .banner .menudivright-r-div .InformationCenter-div .noticeTips {
  background: #ff8013;
  color: #fff
}

.black .el-header .banner .menudivright-r-div .InformationCenter-div .noticeTips:hover {
  opacity: inherit;
  color: #fff
}

.black .el-header .banner .menudivright-r-div .backold-div {
  color: #777;
  opacity: inherit
}

.black .el-header .banner .menudivright-r-div .backold-div:hover {
  opacity: inherit;
  color: #bfbfbf
}

.exploreTip {
  height: 52px;
  background-color: #fbbf30;
  width: 100%;
  text-align: center;
  line-height: 52px;
  font-size: 16px;
  position: relative;
  z-index: 33;
  border-bottom: 1px solid #ccc;
  font-family: Microsoft Yahei
}

.exploreTip div {
  color: #a77600
}

.exploreTip div .browser-download {
  position: relative;
  cursor: pointer;
  color: #fff
}

.exploreTip div .browser-download .browser-version-list {
  position: absolute;
  top: 20px;
  left: 50%;
  margin-left: -48px;
  display: none
}

.exploreTip div .browser-download .browser-version-list li {
  width: 96px;
  height: 40px
}

.exploreTip div .browser-download .browser-version-list li a {
  display: block;
  background: #000;
  line-height: 40px;
  text-decoration: none;
  font-size: 14px
}

.exploreTip div .browser-download .browser-version-list .arrow {
  width: 16px;
  height: 8px;
  margin-left: 40px;
  background: url(//image.zhihuishu.com/testzhs/ablecommons/demo/201704/0b241b0%E2%80%A6.png) no-repeat
}

.exploreTip .hint_delete {
  position: absolute;
  top: 0;
  right: 40px
}

.exploreTip .hint_delete a {
  display: block;
  width: 78px;
  height: 26px;
  margin-top: 13px;
  font-size: 14px;
  text-decoration: none;
  color: #fbbf30;
  text-align: center;
  line-height: 26px;
  background: #fff;
  border-radius: 13px
}

.dialog-abnormal-behavior p[data-v-20d74199] {
  font-family: PingFangSC-Semibold;
  font-size: 17px;
  color: #111;
  text-align: center
}

.dialog-abnormal-behavior .footer[data-v-20d74199] {
  margin-top: 30px;
  display: flex;
  align-items: center;
  justify-content: center
}

.dialog-abnormal-behavior .footer .s1[data-v-20d74199] {
  margin-right: 20px;
  width: 134px;
  height: 44px;
  text-align: center;
  line-height: 44px;
  background: #fff;
  border: 1px solid #ededed;
  border-radius: 8px;
  font-size: 17px;
  color: #2a2a2a;
  font-family: PingFangSC-Regular
}

.dialog-abnormal-behavior .footer[data-v-20d74199] :hover {
  cursor: pointer
}

.dialog-abnormal-behavior .footer .s2[data-v-20d74199] {
  width: 134px;
  height: 44px;
  text-align: center;
  line-height: 44px;
  background: #5d82ff;
  border-radius: 8px;
  font-size: 17px;
  color: #fff;
  font-family: PingFangSC-Regular
}

.dialog-abnormal-behavior .footer .s2[data-v-20d74199] :hover {
  cursor: pointer
}

.el-dialog .el-dialog__header {
  display: flex;
  align-items: center
}

.dialog-abnormal-behavior[data-v-33d7c538] {
  border-radius: 16px
}

.dialog-abnormal-behavior .el-dialog__body[data-v-33d7c538] {
  padding: 20px
}

.dialog-abnormal-behavior .header-title[data-v-33d7c538] {
  line-height: 24px;
  clear: both;
  zoom: 1;
  height: 24px
}

.dialog-abnormal-behavior .header-title i[data-v-33d7c538] {
  float: right;
  font-size: 16px;
  cursor: pointer
}

.dialog-abnormal-behavior .header-title span[data-v-33d7c538] {
  float: left;
  font-size: 17px;
  color: #111;
  line-height: 24px
}

.dialog-abnormal-behavior .main-box[data-v-33d7c538] {
  padding: 0 20px
}

.dialog-abnormal-behavior .main-box .tips[data-v-33d7c538] {
  font-size: 17px;
  color: #111
}

.dialog-abnormal-behavior .main-box .form-box[data-v-33d7c538] {
  padding: 30px 0;
  width: 320px;
  margin: 0 auto
}

.dialog-abnormal-behavior .main-box .from-item[data-v-33d7c538] {
  height: 70px;
  clear: both;
  overflow: hidden
}

.dialog-abnormal-behavior .main-box .from-item .input-sty[data-v-33d7c538] {
  display: block;
  float: left;
  width: 180px;
  height: 40px;
  background: #eeeef5;
  border-radius: 8px;
  border: none;
  padding: 0 15px;
  color: #111;
  font-size: 14px
}

.dialog-abnormal-behavior .main-box .from-item .code-imgage[data-v-33d7c538], .dialog-abnormal-behavior .main-box .from-item .message-btn[data-v-33d7c538] {
  display: block;
  width: 100px;
  height: 40px;
  float: right;
  border-radius: 8px;
  border: none
}

.dialog-abnormal-behavior .main-box .from-item .message-btn[data-v-33d7c538] {
  color: #fff
}

.dialog-abnormal-behavior .main-box .submit-btn[data-v-33d7c538] {
  width: 120px;
  height: 44px;
  display: block;
  margin: 0 auto;
  font-size: 17px;
  border-radius: 8px;
  color: #fff;
  border: none
}

.dialog-abnormal-behavior .main-box .active-color[data-v-33d7c538] {
  background: #5d82ff;
  cursor: pointer
}

.dialog-abnormal-behavior .main-box .wait-color[data-v-33d7c538] {
  background: #6f7bb2;
  cursor: not-allowed
}

.dialog-abnormal-behavior .main-box .disable-color[data-v-33d7c538] {
  background: #ccc;
  cursor: not-allowed
}

.video-study {
  height: 100%;
  overflow: hidden
}

.video-study .box-content {
  margin-top: 60px;
  position: relative;
  height: 100%;
  min-width: 1200px
}

.video-study .box-content .box-left {
  width: calc(100% - 340px);
  height: 100%;
  background: #000;
  position: relative
}

.video-study .box-content .box-left .left-top {
  background: #f6f6f6;
  box-shadow: inset -1px 0 0 0 #ededed;
  right: 340px;
  height: 40px;
  line-height: 40px;
  position: absolute;
  left: 0;
  top: 0;
  padding: 0 35px 0 60px;
  z-index: 2;
  width: 100%;
  box-sizing: border-box
}

.video-study .box-content .box-left .left-top .videotop_lesson {
  text-align: right
}

.video-study .box-content .box-left .left-top .videotop_lesson, .video-study .box-content .box-left .left-top .videotop_lesson_tit {
  height: 40px;
  line-height: 40px;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  display: inline-block;
  font-size: 12px;
  color: #2a2a2a
}

.video-study .box-content .box-left .left-top .videotop_lesson_tit {
  max-width: 400px;
  margin-left: 5px
}

.video-study .box-content .box-left .left-top .videotop_all ul li {
  float: left;
  margin: 6px 5px 0 0;
  cursor: pointer;
  list-style: none;
  height: 30px;
  line-height: 30px;
  font-size: 12px;
  text-align: right;
  padding-left: 14px;
  padding-right: 10px
}

.video-study .box-content .box-left .left-top .videotop_all ul li em {
  margin-top: 0;
  margin-right: 3px;
  color: #d8d8d8
}

.video-study .box-content .box-left .left-top .videotop_all ul li span {
  color: #777
}

.video-study .box-content .box-left .left-top .videotop_all ul li:hover span {
  color: #2a2a2a
}

.video-study .box-content .box-left .limitInfo {
  position: absolute;
  transform: translate(-50%, -50%);
  -webkit-transform: translate(-50%, -50%);
  -moz-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  -o-transform: translate(-50%, -50%);
  background: rgba(42, 42, 42, .95);
  border-radius: 30px;
  width: 630px;
  top: 50%;
  left: 50%;
  box-sizing: border-box
}

.video-study .box-content .box-left .limitInfo .title {
  line-height: 30px;
  color: #ededed;
  font-size: 18px;
  text-align: center;
  margin-top: 30px
}

.video-study .box-content .box-left .limitInfo .limit-tips {
  line-height: 20px;
  margin-top: 20px;
  color: #bfbfbf;
  font-size: 14px;
  text-align: center
}

.video-study .box-content .box-left .limitInfo ul {
  margin-top: 5px;
  margin-bottom: 20px
}

.video-study .box-content .box-left .limitInfo ul li {
  line-height: 48px;
  color: #fff;
  font-size: 24px;
  text-align: center
}

.video-study .box-content .box-left .threed-box {
  position: absolute;
  bottom: 120px;
  left: 40px;
  height: 32px;
  background: hsla(0, 0%, 100%, .9);
  border-radius: 21px;
  width: 32px;
  overflow: hidden;
  clear: both;
  transition: .5s;
  cursor: pointer;
  z-index: 2
}

.video-study .box-content .box-left .threed-box .icon {
  width: 24px;
  height: 24px;
  float: left;
  border: 4px solid #fff;
  margin-right: 5px;
  border-radius: 50px
}

.video-study .box-content .box-left .threed-box span {
  margin: 0 5px;
  font-size: 14px;
  line-height: 32px;
  color: #666;
  max-width: 145px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  display: block;
  float: left
}

.video-study .box-content .box-left .threed-box .iconfont {
  font-size: 20px;
  transform: rotateY(180deg);
  float: right;
  color: #666;
  margin-right: 8px;
  margin-top: 5px
}

.video-study .box-content .box-left .three-show {
  width: 220px
}

.video-study .box-content .box-left .video-topic {
  position: absolute;
  bottom: 10px;
  width: 100%;
  height: 20px;
  right: 5px;
  z-index: 2
}

.video-study .box-content .box-left .video-topic ul {
  margin-right: 10px
}

.video-study .box-content .box-left .video-topic ul li {
  cursor: pointer;
  background: #fff;
  width: 5px;
  height: 5px;
  border-radius: 5px;
  position: absolute
}

.video-study .box-content .box-left .video-topic ul li span {
  display: block;
  width: 100%;
  height: 5px;
  position: relative
}

.video-study .box-content .box-left .video-topic ul li span .el-popover {
  left: 0;
  bottom: 10px
}

.video-study .box-content .box-right {
  position: absolute;
  height: 100%;
  top: 0;
  bottom: 0;
  right: 0;
  width: 340px
}

.video-study .box-content .box-right .newListTest {
  padding: 0 15px;
  overflow: hidden;
  clear: both
}

.video-study .box-content .box-right .newListTest li {
  margin-right: 5px;
  height: 80px;
  list-style: none;
  float: left;
  width: 100px;
  text-align: center;
  line-height: 30px;
  font-size: 12px;
  color: #bfbfbf;
  cursor: pointer
}

.video-study .box-content .box-right .newListTest li:nth-child(3n) {
  margin-right: 0
}

.video-study .box-content .box-right .newListTest li:hover {
  background: #ededed
}

.video-study .box-content .box-right .newListTest li a {
  font-size: 12px;
  color: #777;
  display: inline-block;
  line-height: 19px;
  margin-top: 10px
}

.video-study .box-content .box-right .newListTest li a .icon {
  width: 40px;
  height: 40px
}

.video-study .box-content .box-right .topicTitle {
  width: 340px;
  height: 40px;
  background: #f6f6f6
}

.video-study .box-content .box-right .topicTitle ul {
  margin-left: 20px
}

.video-study .box-content .box-right .topicTitle ul .tabTitle {
  font-size: 14px;
  color: #2a2a2a;
  line-height: 40px
}

.video-study .box-content .box-right .list {
  position: relative;
  padding-bottom: 20px;
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/892e66724a934d7291452c71a992f244.png) 68px 0 repeat-y
}

.video-study .box-content .box-right .list .position_first_bg {
  position: absolute;
  z-index: 1;
  left: 68px;
  top: -11px;
  display: inline-block;
  height: 20px;
  width: 2px
}

.video-study .box-content .box-right .list li {
  position: relative;
  padding: 7px 10px 7px 3px !important;
  height: 36px;
  font-family: Tahoma;
  width: 100%;
  font-size: 12px
}

.video-study .box-content .box-right .list li:hover {
  background: #ededed;
  font-size: 12px;
  color: #2a2a2a
}

.video-study .box-content .box-right .list li:hover .chapter-em {
  background: url(https://image.zhihuishu.com/zhs_yufa_150820/ablecommons/demo/201910/2644659e82f34d9ea62a0f436f0ac1e9.png) no-repeat
}

.video-study .box-content .box-right .list li .catalogue_title3 {
  font-size: 12px;
  color: #777;
  line-height: 38px;
  height: 26px;
  display: inline-block;
  text-align: right;
  width: 50px;
  padding-right: 7px;
  overflow: hidden
}

.video-study .box-content .box-right .list li .catalogue_title4 {
  font-size: 12px;
  color: #999;
  line-height: 38px;
  height: 26px;
  display: inline-block;
  text-align: right;
  width: 50px;
  padding-right: 7px;
  overflow: hidden
}

.video-study .box-content .box-right .list li .cataloguediv-l {
  width: 50px;
  padding-right: 18px
}

.video-study .box-content .box-right .list li .time_ico_box {
  display: block;
  height: 20px;
  margin-left: 1px;
  margin-right: 14px
}

.video-study .box-content .box-right .list li .catalogue_title {
  font-size: 12px;
  color: #2a2a2a;
  margin-bottom: 5px;
  line-height: 18px;
  display: block;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  width: 200px
}

.video-study .box-content .box-right .list li .small-lesson {
  line-height: 36px
}

.video-study .box-content .box-right .list li .cataloguediv-c {
  width: 210px;
  margin-left: 20px
}

.video-study .box-content .box-right .list li .time_ico_half {
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/5efaa4c4040e4042bde4fc1fa61a8e10.png) no-repeat;
  display: inline-block;
  height: 12px;
  margin: 1px 5px 0 0;
  width: 12px
}

.video-study .box-content .box-right .list li .time_icofinish {
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/5b3134c2c263451c8d45cb477b5f79e4.png) no-repeat;
  position: absolute;
  right: 24px;
  top: 17px;
  width: 17px;
  height: 17px;
  display: block
}

.video-study .box-content .box-right .list li .el-progress {
  position: absolute;
  right: 25px;
  top: 10px
}

.video-study .box-content .box-right .list li .el-progress .el-progress-circle {
  height: 16px !important;
  width: 16px !important
}

.video-study .box-content .box-right .list li .el-progress .el-progress__text {
  font-size: 12px !important;
  color: #3d84ff
}

.video-study .box-content .box-right .list li .el-progress .el-progress-circle__track {
  stroke: #3d84ff;
  opacity: .3
}

.video-study .box-content .box-right .list li .el-progress .el-progress-circle__path {
  stroke: #3d84ff
}

.video-study .box-content .box-right .list li .progress-num {
  position: absolute;
  right: 20px;
  top: 28px;
  font-size: 12px !important;
  color: #3d84ff
}

.video-study .box-content .box-right .list li .time {
  color: #777;
  font-size: 12px
}

.video-study .box-content .box-right .list li .learningPercentage-div {
  width: 20px;
  height: 20px;
  position: relative;
  right: 14px
}

.video-study .box-content .box-right .list li .learningPercentage-div .learningPercentage-span {
  position: absolute;
  bottom: -16px;
  left: 0;
  font-size: 12px;
  color: #3d84ff
}

.video-study .box-content .box-right .list li .learningPercentage-div .progressCricle {
  width: 20px;
  height: 20px
}

.video-study .box-content .box-right .list li .Sectionmark-em {
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/5e635034f9e24ab48c97fc7fcf1b516a.png) no-repeat;
  width: 11px;
  height: 11px;
  display: inline-block;
  position: absolute;
  left: 64px;
  top: 20px
}

.video-study .box-content .box-right .list .chapter-test {
  padding-left: 61px !important;
  cursor: pointer;
  line-height: 40px;
  line-height: 37px;
  color: #2a2a2a;
  position: relative
}

.video-study .box-content .box-right .list .chapter-test .name {
  margin-left: 30px;
  color: #2a2a2a;
  font-size: 12px
}

.video-study .box-content .box-right .list .chapter-test .iconfont {
  padding: 0 20px;
  cursor: pointer;
  position: absolute;
  right: 62px;
  top: 8px;
  color: #666
}

.video-study .box-content .box-right .list .chapter-test .finish {
  height: 17px;
  width: 17px;
  display: block;
  cursor: pointer;
  position: absolute;
  right: 82px;
  top: 17px;
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/5b3134c2c263451c8d45cb477b5f79e4.png) no-repeat
}

.video-study .box-content .box-right .list .video {
  cursor: pointer
}

.video-study .box-content .box-right .list .font_gray_inclined .catalogue_title {
  margin-top: 10px;
  font-size: 14px;
  font-weight: 700
}

.video-study .box-content .box-right .list .font_gray_inclined .chapter-em {
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/7943740388164e14980b89c244f35c58.png) no-repeat;
  width: 11px;
  height: 11px;
  display: inline-block;
  margin: 13px 0 0 3px
}

.video-study .box-content .box-right .list .current_play {
  background: rgba(61, 132, 255, .15)
}

.video-study .box-content .box-right .list .current_play .catalogue_title3, .video-study .box-content .box-right .list .current_play .catalogue_title4 {
  color: #3d84ff
}

.video-study .box-content .box-right .list .current_play .catalogue_title {
  color: #3d84ff;
  font-weight: 700
}

.video-study .box-content .box-right .list .current_play .time_ico_half {
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/51172bf9b834437492667911fb2a6b68.png) no-repeat
}

.video-study .box-content .box-right .list .current_play .time {
  font-size: 12px;
  color: rgba(61, 132, 255, .8);
  letter-spacing: .1px
}

.video-study .el-scrollbar .el-scrollbar__wrap {
  overflow-x: hidden
}

.video-study .el-scrollbar .el-scrollbar__bar {
  right: 0
}

.video-study .el-scrollbar .is-horizontal {
  opacity: 0 !important;
  display: none
}

.video-study .el-scrollbar .el-scrollbar__thumb {
  background: #bfbfbf;
  width: 4px
}

.video-study .dialog-aberrant .el-dialog, .video-study .dialog-back .el-dialog, .video-study .dialog-class .el-dialog, .video-study .dialog-img .el-dialog, .video-study .dialog-look-ans .el-dialog, .video-study .dialog-read .el-dialog, .video-study .dialog-teach .el-dialog, .video-study .dialog-test .el-dialog, .video-study .dialog-tips .el-dialog, .video-study .dialog-warn .el-dialog, .video-study .read-learn .el-dialog {
  width: 400px;
  height: 250px;
  border-radius: 2px
}

.video-study .dialog-aberrant .el-dialog .el-dialog__header, .video-study .dialog-back .el-dialog .el-dialog__header, .video-study .dialog-class .el-dialog .el-dialog__header, .video-study .dialog-img .el-dialog .el-dialog__header, .video-study .dialog-look-ans .el-dialog .el-dialog__header, .video-study .dialog-read .el-dialog .el-dialog__header, .video-study .dialog-teach .el-dialog .el-dialog__header, .video-study .dialog-test .el-dialog .el-dialog__header, .video-study .dialog-tips .el-dialog .el-dialog__header, .video-study .dialog-warn .el-dialog .el-dialog__header, .video-study .read-learn .el-dialog .el-dialog__header {
  padding: 20px 30px;
  padding-bottom: 15px
}

.video-study .dialog-aberrant .el-dialog .el-dialog__title, .video-study .dialog-back .el-dialog .el-dialog__title, .video-study .dialog-class .el-dialog .el-dialog__title, .video-study .dialog-img .el-dialog .el-dialog__title, .video-study .dialog-look-ans .el-dialog .el-dialog__title, .video-study .dialog-read .el-dialog .el-dialog__title, .video-study .dialog-teach .el-dialog .el-dialog__title, .video-study .dialog-test .el-dialog .el-dialog__title, .video-study .dialog-tips .el-dialog .el-dialog__title, .video-study .dialog-warn .el-dialog .el-dialog__title, .video-study .read-learn .el-dialog .el-dialog__title {
  font-weight: 700
}

.video-study .dialog-aberrant .el-dialog .el-dialog__headerbtn, .video-study .dialog-back .el-dialog .el-dialog__headerbtn, .video-study .dialog-class .el-dialog .el-dialog__headerbtn, .video-study .dialog-img .el-dialog .el-dialog__headerbtn, .video-study .dialog-look-ans .el-dialog .el-dialog__headerbtn, .video-study .dialog-read .el-dialog .el-dialog__headerbtn, .video-study .dialog-teach .el-dialog .el-dialog__headerbtn, .video-study .dialog-test .el-dialog .el-dialog__headerbtn, .video-study .dialog-tips .el-dialog .el-dialog__headerbtn, .video-study .dialog-warn .el-dialog .el-dialog__headerbtn, .video-study .read-learn .el-dialog .el-dialog__headerbtn {
  right: 30px
}

.video-study .dialog-aberrant .el-dialog .el-dialog__close, .video-study .dialog-back .el-dialog .el-dialog__close, .video-study .dialog-class .el-dialog .el-dialog__close, .video-study .dialog-img .el-dialog .el-dialog__close, .video-study .dialog-look-ans .el-dialog .el-dialog__close, .video-study .dialog-read .el-dialog .el-dialog__close, .video-study .dialog-teach .el-dialog .el-dialog__close, .video-study .dialog-test .el-dialog .el-dialog__close, .video-study .dialog-tips .el-dialog .el-dialog__close, .video-study .dialog-warn .el-dialog .el-dialog__close, .video-study .read-learn .el-dialog .el-dialog__close {
  color: #777;
  font-size: 18px
}

.video-study .dialog-aberrant .el-dialog .el-dialog__body, .video-study .dialog-back .el-dialog .el-dialog__body, .video-study .dialog-class .el-dialog .el-dialog__body, .video-study .dialog-img .el-dialog .el-dialog__body, .video-study .dialog-look-ans .el-dialog .el-dialog__body, .video-study .dialog-read .el-dialog .el-dialog__body, .video-study .dialog-teach .el-dialog .el-dialog__body, .video-study .dialog-test .el-dialog .el-dialog__body, .video-study .dialog-tips .el-dialog .el-dialog__body, .video-study .dialog-warn .el-dialog .el-dialog__body, .video-study .read-learn .el-dialog .el-dialog__body {
  padding: 0 64px;
  text-align: center
}

.video-study .dialog-aberrant .el-dialog .el-dialog__body img, .video-study .dialog-back .el-dialog .el-dialog__body img, .video-study .dialog-class .el-dialog .el-dialog__body img, .video-study .dialog-img .el-dialog .el-dialog__body img, .video-study .dialog-look-ans .el-dialog .el-dialog__body img, .video-study .dialog-read .el-dialog .el-dialog__body img, .video-study .dialog-teach .el-dialog .el-dialog__body img, .video-study .dialog-test .el-dialog .el-dialog__body img, .video-study .dialog-tips .el-dialog .el-dialog__body img, .video-study .dialog-warn .el-dialog .el-dialog__body img, .video-study .read-learn .el-dialog .el-dialog__body img {
  margin-bottom: 5px
}

.video-study .dialog-aberrant .el-dialog .el-dialog__body p, .video-study .dialog-back .el-dialog .el-dialog__body p, .video-study .dialog-class .el-dialog .el-dialog__body p, .video-study .dialog-img .el-dialog .el-dialog__body p, .video-study .dialog-look-ans .el-dialog .el-dialog__body p, .video-study .dialog-read .el-dialog .el-dialog__body p, .video-study .dialog-teach .el-dialog .el-dialog__body p, .video-study .dialog-test .el-dialog .el-dialog__body p, .video-study .dialog-tips .el-dialog .el-dialog__body p, .video-study .dialog-warn .el-dialog .el-dialog__body p, .video-study .read-learn .el-dialog .el-dialog__body p {
  font-size: 14px;
  color: #2a2a2a;
  line-height: 24px
}

.video-study .dialog-aberrant .el-dialog .el-dialog__footer, .video-study .dialog-back .el-dialog .el-dialog__footer, .video-study .dialog-class .el-dialog .el-dialog__footer, .video-study .dialog-img .el-dialog .el-dialog__footer, .video-study .dialog-look-ans .el-dialog .el-dialog__footer, .video-study .dialog-read .el-dialog .el-dialog__footer, .video-study .dialog-teach .el-dialog .el-dialog__footer, .video-study .dialog-test .el-dialog .el-dialog__footer, .video-study .dialog-tips .el-dialog .el-dialog__footer, .video-study .dialog-warn .el-dialog .el-dialog__footer, .video-study .read-learn .el-dialog .el-dialog__footer {
  padding: 0;
  text-align: center;
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  -webkit-transform: translateX(-50%);
  -moz-transform: translateX(-50%);
  -ms-transform: translateX(-50%);
  -o-transform: translateX(-50%)
}

.video-study .dialog-aberrant .el-dialog .el-dialog__footer .btn, .video-study .dialog-back .el-dialog .el-dialog__footer .btn, .video-study .dialog-class .el-dialog .el-dialog__footer .btn, .video-study .dialog-img .el-dialog .el-dialog__footer .btn, .video-study .dialog-look-ans .el-dialog .el-dialog__footer .btn, .video-study .dialog-read .el-dialog .el-dialog__footer .btn, .video-study .dialog-teach .el-dialog .el-dialog__footer .btn, .video-study .dialog-test .el-dialog .el-dialog__footer .btn, .video-study .dialog-tips .el-dialog .el-dialog__footer .btn, .video-study .dialog-warn .el-dialog .el-dialog__footer .btn, .video-study .read-learn .el-dialog .el-dialog__footer .btn {
  background: #3d84ff;
  width: 120px;
  height: 40px;
  text-align: center;
  color: #fff;
  border: 0;
  border-radius: 0
}

.video-study .dialog-aberrant .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-back .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-class .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-img .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-look-ans .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-read .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-teach .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-test .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-tips .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-warn .el-dialog .el-dialog__footer .btn:hover, .video-study .read-learn .el-dialog .el-dialog__footer .btn:hover {
  background: rgba(61, 132, 255, .8)
}

.video-study .dialog-tips .el-dialog .el-dialog__body {
  padding: 0 26px
}

.video-study .dialog-aberrant .el-dialog {
  height: 300px
}

.video-study .dialog-aberrant .el-dialog .el-dialog__body {
  padding: 0 26px
}

.video-study .dialog-back .el-dialog .el-dialog__body {
  margin-top: 20px;
  padding: 0 35px;
  text-align: left
}

.video-study .dialog-back .el-dialog .el-dialog__body p {
  font-size: 16px;
  color: #2a2a2a;
  line-height: 24px
}

.video-study .aberrant {
  position: absolute;
  transform: translate(-50%, -50%);
  -webkit-transform: translate(-50%, -50%);
  -moz-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  -o-transform: translate(-50%, -50%);
  background: rgba(42, 42, 42, .95);
  border-radius: 30px;
  width: 630px;
  top: 50%;
  left: 50%;
  box-sizing: border-box;
  z-index: 101
}

.video-study .aberrant .title {
  line-height: 30px;
  color: #ededed;
  font-size: 18px;
  text-align: center;
  margin-top: 30px;
  padding: 0 40px
}

.video-study .aberrant .limit-tips {
  line-height: 20px;
  margin-top: 20px;
  color: #bfbfbf;
  font-size: 14px;
  text-align: center
}

.video-study .aberrant ul {
  margin-top: 5px;
  margin-bottom: 20px
}

.video-study .aberrant ul li {
  line-height: 48px;
  color: #fff;
  font-size: 24px;
  text-align: center
}

.video-study .aberrant a {
  display: block;
  background: #3d84ff;
  width: 120px;
  height: 40px;
  text-align: center;
  color: #fff;
  border: 0;
  border-radius: 0;
  margin: 0 auto;
  margin-bottom: 20px;
  line-height: 40px;
  cursor: pointer;
  z-index: 20
}

.video-study .dialog-teach .el-dialog, .video-study .dialog-test .el-dialog, .video-study .dialog-warn .el-dialog {
  height: 480px;
  width: 630px
}

.video-study .dialog-teach .el-dialog .el-dialog__body, .video-study .dialog-test .el-dialog .el-dialog__body, .video-study .dialog-warn .el-dialog .el-dialog__body {
  padding: 0 90px;
  text-align: center;
  margin-top: 30px
}

.video-study .dialog-teach .el-dialog .el-dialog__body p, .video-study .dialog-test .el-dialog .el-dialog__body p, .video-study .dialog-warn .el-dialog .el-dialog__body p {
  font-size: 14px;
  color: #2a2a2a;
  line-height: 24px;
  text-align: left
}

.video-study .dialog-teach .el-dialog .el-dialog__body {
  padding: 0;
  text-align: left;
  margin-top: 30px
}

.video-study .dialog-teach .el-dialog .el-dialog__body h2 {
  text-align: center;
  line-height: 30px;
  font-size: 18px;
  color: #2a2a2a;
  margin-bottom: 20px
}

.video-study .dialog-teach .el-dialog .el-dialog__body h3 {
  text-align: left;
  line-height: 20px;
  font-size: 14px;
  color: #2a2a2a
}

.video-study .dialog-teach .el-dialog .el-dialog__body .teach-box {
  padding: 0 90px
}

.video-study .dialog-teach .el-dialog .el-dialog__body ul li p {
  margin: 12px 0;
  font-size: 14px;
  color: #2a2a2a;
  line-height: 24px;
  text-align: left;
  word-wrap: break-word
}

.video-study .dialog-test .el-dialog .el-dialog__header {
  border-bottom: 1px solid #ededed
}

.video-study .dialog-test .el-dialog .el-dialog__header h4 {
  font-size: 18px;
  color: #2a2a2a;
  line-height: 30px
}

.video-study .dialog-test .el-dialog .el-dialog__header p {
  font-size: 12px;
  color: #777;
  position: relative;
  line-height: 18px
}

.video-study .dialog-test .el-dialog .el-dialog__body {
  margin-top: 0;
  padding: 0
}

.video-study .dialog-test .el-dialog .el-scrollbar__wrap {
  padding-top: 30px
}

.video-study .dialog-test .el-dialog .radio {
  margin: 0 90px;
  margin-bottom: 90px
}

.video-study .dialog-test .el-dialog .topic-title {
  font-size: 14px;
  line-height: 24px;
  color: #333;
  margin-bottom: 10px;
  position: relative
}

.video-study .dialog-test .el-dialog .topic-title .title-tit {
  color: #151515;
  font-weight: 600
}

.video-study .dialog-test .el-dialog .topic-title img {
  max-width: 100%;
  height: auto !important;
  -o-object-fit: cover;
  object-fit: cover;
  vertical-align: middle
}

.video-study .dialog-test .el-dialog .topic-title .error, .video-study .dialog-test .el-dialog .topic-title .right {
  color: #00d789;
  margin-right: 12px;
  position: absolute;
  left: -48px
}

.video-study .dialog-test .el-dialog .topic-title .error .iconfont, .video-study .dialog-test .el-dialog .topic-title .right .iconfont {
  font-size: 14px;
  position: absolute;
  left: -20px
}

.video-study .dialog-test .el-dialog .topic-title .error {
  color: #f94f17
}

.video-study .dialog-test .el-dialog .topic-list {
  margin-left: 0;
  list-style: none
}

.video-study .dialog-test .el-dialog .topic-list .topic-item {
  font-size: 14px;
  color: #2a2a2a;
  padding: 13px 20px 13px 60px;
  position: relative;
  line-height: 24px;
  word-break: break-all;
  cursor: pointer
}

.video-study .dialog-test .el-dialog .topic-list .topic-item .topic-option {
  position: absolute;
  top: 50%;
  margin-top: -9px;
  width: 18px;
  height: 18px;
  text-align: center;
  left: 15px
}

.video-study .dialog-test .el-dialog .topic-list .topic-item .topic-option-item {
  position: absolute;
  top: 50%;
  margin-top: -12px;
  text-align: center;
  left: 40px;
  color: #2a2a2a;
  font-size: 14px
}

.video-study .dialog-test .el-dialog .topic-list .topic-item .active, .video-study .dialog-test .el-dialog .topic-list .topic-item .iconxuanzhong {
  color: #3d84ff
}

.video-study .dialog-test .el-dialog .topic-list .topic-item .item-topic {
  text-align: left
}

.video-study .dialog-test .el-dialog .topic-list .topic-item .item-topic p {
  display: inline-block
}

.video-study .dialog-test .el-dialog .topic-list .topic-item .item-topic img {
  max-width: 100%;
  height: auto !important;
  -o-object-fit: cover;
  object-fit: cover;
  vertical-align: middle
}

.video-study .dialog-test .el-dialog .answer-tit {
  margin-top: 13px;
  margin-bottom: 26px;
  font-size: 14px;
  color: #2a2a2a;
  font-weight: 600
}

.video-study .dialog-test .el-dialog .answer {
  margin-bottom: 28px;
  font-size: 14px;
  color: #2a2a2a
}

.video-study .dialog-test .el-dialog .answer span {
  color: #3d84ff
}

.video-study .dialog-test .el-dialog .answer-ans {
  font-size: 14px;
  color: #2a2a2a;
  text-align: left
}

.video-study .dialog-test .el-dialog .answer-ans ul {
  width: 535px
}

.video-study .dialog-test .el-dialog .answer-ans ul li {
  float: left;
  margin-right: 15px
}

.video-study .dialog-test .el-dialog .answer-ans ul li img {
  background-size: cover;
  width: 120px;
  height: 120px
}

.video-study .dialog-test .el-dialog .el-dialog__footer .dialog-footer .btn {
  height: 22px;
  line-height: 22px;
  color: #3d4059;
  border-radius: 12px;
  border: 1px solid #d8d8d8;
  background: #fff;
  font-size: 14px;
  width: 100px;
  cursor: pointer
}

.video-study .dialog-img .el-dialog {
  height: 480px;
  width: 630px
}

.video-study .dialog-img .el-dialog .el-dialog__body {
  padding: 0 30px;
  text-align: center;
  margin-top: 10px;
  height: 360px
}

.video-study .dialog-img .el-dialog .el-dialog__body img {
  -o-object-fit: cover;
  object-fit: cover;
  max-width: 570px;
  height: 100%
}

.video-study .read-learn .el-dialog {
  height: 300px;
  width: 440px
}

.video-study .read-learn .el-dialog .el-dialog__body {
  padding: 0 30px;
  text-align: center;
  margin-top: 10px;
  height: 360px
}

.video-study .read-learn .el-dialog .el-dialog__body p {
  text-align: left
}

.video-study .read-learn .el-dialog .el-dialog__body p span {
  display: block;
  color: #3d84ff;
  margin-top: 10px
}

.video-study .dialog-class .el-dialog {
  height: 430px
}

.video-study .dialog-class .el-dialog .el-dialog__body {
  text-align: left;
  padding: 0
}

.video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .el-scrollbar__wrap {
  padding: 0 30px
}

.video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-class .title, .video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-teacher .title {
  line-height: 24px;
  color: #2a2a2a;
  font-size: 14px;
  font-weight: 700;
  margin-bottom: 10px
}

.video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-class .title span, .video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-teacher .title span {
  height: 14px;
  width: 2px;
  background: #3d84ff;
  float: left;
  margin-right: 5px;
  margin-top: 5px
}

.video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-class .name, .video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-teacher .name {
  line-height: 24px;
  font-size: 14px;
  color: #2a2a2a;
  margin-bottom: 30px
}

.video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-class .teacher-info, .video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-teacher .teacher-info {
  margin-bottom: 21px
}

.video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-class .teacher-info span, .video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-teacher .teacher-info span {
  display: block
}

.video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-class .teacher-info .name, .video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-teacher .teacher-info .name {
  line-height: 24px;
  font-size: 14px;
  color: #2a2a2a;
  margin-bottom: 5px
}

.video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-class .teacher-info .num, .video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-teacher .teacher-info .num {
  font-size: 12px;
  color: #777;
  line-height: 18px
}

.video-study .dialog .mask {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  opacity: .5;
  background: #000;
  z-index: 100
}

.video-study .dialog-read {
  width: 630px;
  height: 480px;
  top: 50%;
  left: 50%;
  position: fixed;
  transform: translate(-50%, -50%);
  background: #fff;
  z-index: 101
}

.video-study .dialog-read .el-dialog__header {
  border-bottom: 1px solid #ededed;
  padding: 20px 30px;
  padding-bottom: 15px;
  position: relative
}

.video-study .dialog-read .el-dialog__header h4 {
  font-size: 18px;
  color: #2a2a2a;
  line-height: 30px
}

.video-study .dialog-read .el-dialog__header p {
  font-size: 12px;
  color: #3d84ff;
  position: relative;
  line-height: 18px
}

.video-study .dialog-read .el-dialog__header .iconguanbi {
  position: absolute;
  top: 30px;
  right: 30px;
  font-size: 20px;
  color: #777;
  cursor: pointer
}

.video-study .dialog-read .el-dialog__body {
  padding: 0
}

.video-study .dialog-look-ans .el-dialog {
  position: relative
}

.video-study .dialog-look-ans .el-dialog .el-dialog__body {
  padding: 0 65px
}

.video-study .dialog-look-ans .el-dialog .el-dialog__footer {
  padding: 0;
  text-align: center;
  position: absolute;
  bottom: 20px;
  width: 100%
}

.video-study .dialog-look-ans .el-dialog .el-dialog__footer .btn {
  background: #3d84ff;
  width: 120px;
  height: 40px;
  text-align: center;
  color: #fff;
  border: 1px solid #3d84ff;
  border-radius: 0
}

.video-study .dialog-look-ans .el-dialog .el-dialog__footer .btn:hover {
  background: rgba(61, 132, 255, .8)
}

.video-study .dialog-look-ans .el-dialog .el-dialog__footer .cancel {
  background: #fff;
  border: 1px solid #ededed;
  color: #2a2a2a
}

.video-study .dialog-look-ans .el-dialog .el-dialog__footer .cancel:hover {
  background: #ededed
}

.video-study .dialog-look-habit .el-dialog {
  width: 500px;
  height: 346px;
  border-radius: 2px
}

.video-study .dialog-look-habit .el-dialog .el-dialog__header {
  padding: 20px 30px;
  padding-bottom: 15px;
  border-bottom: 1px solid #ededed
}

.video-study .dialog-look-habit .el-dialog .el-dialog__title {
  font-weight: 700
}

.video-study .dialog-look-habit .el-dialog .el-dialog__headerbtn {
  right: 30px
}

.video-study .dialog-look-habit .el-dialog .el-dialog__close {
  color: #777;
  font-size: 18px
}

.video-study .dialog-look-habit .el-dialog .el-dialog__body {
  padding: 0 40px;
  text-align: left;
  margin-top: 20px
}

.video-study .dialog-look-habit .el-dialog .el-dialog__body p {
  font-size: 14px;
  color: #2a2a2a;
  line-height: 24px
}

.video-study .dialog-look-habit .el-dialog .el-dialog__body p a {
  color: #3d84ff;
  cursor: pointer
}

.video-study .dialog-look-habit .el-dialog .el-dialog__footer {
  padding: 0;
  text-align: center;
  position: absolute;
  bottom: 30px;
  left: 50%;
  width: 500px;
  transform: translateX(-50%);
  -webkit-transform: translateX(-50%);
  -moz-transform: translateX(-50%);
  -ms-transform: translateX(-50%);
  -o-transform: translateX(-50%)
}

.video-study .dialog-look-habit .el-dialog .el-dialog__footer .btn {
  background: #3d84ff;
  width: 140px;
  height: 32px;
  line-height: 32px;
  text-align: center;
  color: #fff;
  border: 0;
  padding: 0;
  border-radius: 2px
}

.video-study .dialog-look-habit .el-dialog .el-dialog__footer .btn:hover {
  background: rgba(61, 132, 255, .8)
}

.video-study .dialog-look-habit .el-dialog .habit-teshu {
  margin-top: 10px;
  text-align: left;
  font-size: 12px;
  color: #f94f17;
  line-height: 18px;
  padding: 10px;
  background: #fef5e2
}

.video-study .dialog-learn-habit .el-dialog {
  width: 570px;
  height: 520px;
  border-radius: 2px
}

.video-study .dialog-learn-habit .el-dialog .el-dialog__header {
  padding: 20px 30px;
  padding-bottom: 15px
}

.video-study .dialog-learn-habit .el-dialog .el-dialog__title {
  font-weight: 700
}

.video-study .dialog-learn-habit .el-dialog .el-dialog__headerbtn {
  right: 30px
}

.video-study .dialog-learn-habit .el-dialog .el-dialog__close {
  color: #777;
  font-size: 18px
}

.video-study .dialog-learn-habit .el-dialog .el-dialog__body {
  padding: 0;
  text-align: left
}

.video-study .preschool-Mustread-div {
  padding: 0 30px 55px;
  background: #fff
}

.video-study .preschool-Mustread-div .studyExam-div {
  border-top: 1px solid #ededed;
  border-bottom: 1px solid #ededed;
  padding: 15px 0;
  text-align: center
}

.video-study .preschool-Mustread-div .studyExam-div .studytime-div {
  margin-bottom: 15px
}

.video-study .preschool-Mustread-div .studyExam-div .studytime-div .studytime-p1 {
  color: #333;
  line-height: 26px;
  font-weight: 700;
  font-size: 16px
}

.video-study .preschool-Mustread-div .studyExam-div .studytime-div .studytime-p2 {
  font-size: 12px;
  color: #2a2a2a;
  line-height: 18px;
  margin-top: 5px
}

.video-study .preschool-Mustread-div .studyExam-div .Examtime-div .Examtime-p1 {
  color: #333;
  line-height: 26px;
  font-weight: 700;
  font-size: 16px
}

.video-study .preschool-Mustread-div .studyExam-div .Examtime-div .Examtime-p2 {
  font-size: 12px;
  color: #2a2a2a;
  line-height: 18px;
  margin-top: 5px
}

.video-study .preschool-Mustread-div .studyhint-p {
  font-size: 12px;
  color: #666;
  line-height: 18px;
  margin-top: 10px;
  text-align: center
}

.video-study .AchievementRules-div {
  margin-top: 40px
}

.video-study .AchievementRules-div h1 {
  font-size: 18px;
  color: #000;
  line-height: 30px;
  font-weight: 700
}

.video-study .AchievementRules-div h2 {
  font-size: 14px;
  color: #2a2a2a;
  letter-spacing: .07px;
  line-height: 24px;
  font-weight: 700;
  margin-top: 18px
}

.video-study .AchievementRules-div .p1 {
  font-size: 14px;
  color: #777;
  letter-spacing: .07px;
  line-height: 24px
}

.video-study .AchievementRulesbg-div {
  background: #f7f9fe;
  border-radius: 2px;
  padding: 20px 25px
}

.video-study .AchievementRulesbg-div ul li {
  font-size: 14px;
  color: #777;
  letter-spacing: .07px;
  line-height: 24px
}

.video-study .AchievementRulesbg-div ul .bulefont {
  color: #3d84ff
}

.video-study .AchievementRuleslist {
  margin-bottom: 45px
}

.video-study .nano-content-all {
  height: 370px
}

.video-study .el-pagination {
  margin-bottom: 18px
}

.video-study .el-pagination .el-pager li {
  background: #fff;
  border: 1px solid #ededed;
  border-radius: 12px;
  font-size: 12px;
  color: #2a2a2a
}

.video-study .el-pagination .el-pager .active, .video-study .el-pagination .el-pager li:hover {
  background: #3d84ff;
  color: #fff;
  border: 1px solid #3d84ff
}

.video-study-black .box-content .box-left .left-top {
  background: #1d1d1d;
  box-shadow: inset -1px 0 0 0 #2a2a2a;
  color: #777
}

.video-study-black .box-content .box-left .left-top .videotop_lesson, .video-study-black .box-content .box-left .left-top .videotop_lesson_tit {
  color: #bfbfbf
}

.video-study-black .box-content .box-left .left-top .videotop_all ul li em, .video-study-black .box-content .box-left .left-top .videotop_all ul li span {
  color: #777
}

.video-study-black .box-content .box-left .left-top .videotop_all ul li:hover em, .video-study-black .box-content .box-left .left-top .videotop_all ul li:hover span {
  color: #bfbfbf
}

.video-study-black .box-content .box-right {
  background: #1d1d1d
}

.video-study-black .box-content .box-right .newListTest li {
  color: #777
}

.video-study-black .box-content .box-right .newListTest li:hover {
  background: #2a2a2a
}

.video-study-black .box-content .box-right .newListTest li a {
  color: #777
}

.video-study-black .box-content .box-right .newListTest li a em {
  color: #bfbfbf
}

.video-study-black .box-content .box-right .newListTest li a div {
  margin-top: 5px
}

.video-study-black .box-content .box-right .topicTitle {
  background: #2a2a2a;
  box-shadow: inset 0 -1px 0 0 #2a2a2a
}

.video-study-black .box-content .box-right .topicTitle ul .tabTitle {
  color: #bfbfbf
}

.video-study-black .box-content .box-right .list {
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/2e21819f5b664b67b29113d2ba582974.png) 68px 0 repeat-y
}

.video-study-black .box-content .box-right .list li:hover {
  background: #2a2a2a;
  color: #ededed
}

.video-study-black .box-content .box-right .list li:hover .chapter-em {
  background: url(https://image.zhihuishu.com/zhs_yufa_150820/ablecommons/demo/201910/2592813a3dee4adb9687bd4e4805c8ba.png) no-repeat
}

.video-study-black .box-content .box-right .list li .catalogue_title3 {
  color: #777
}

.video-study-black .box-content .box-right .list li .catalogue_title4 {
  color: #999
}

.video-study-black .box-content .box-right .list li .catalogue_title {
  color: #ededed
}

.video-study-black .box-content .box-right .list li .time {
  color: #777
}

.video-study-black .box-content .box-right .list li .Sectionmark-em {
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/bcefe48e05f44b38ab1bf8615c6ca3d0.png) no-repeat
}

.video-study-black .box-content .box-right .list .chapter-test .name {
  color: #ededed
}

.video-study-black .box-content .box-right .list .chapter-test .iconfont {
  color: #777
}

.video-study-black .box-content .box-right .list .chapter-test .iconyiwancheng {
  color: #3d84ff
}

.video-study-black .box-content .box-right .list .font_gray_inclined .chapter-em {
  background: url(https://image.zhihuishu.com/zhs_yufa_150820/ablecommons/demo/201910/92769ecc02ba46b39d7ae8785def5396.png) no-repeat
}

.video-study-black .box-content .box-right .list .current_play {
  background: rgba(61, 132, 255, .15);
  color: #3d84ff
}

.el-message-box {
  border-radius: 2px
}

.el-message-box .el-message-box__header {
  padding: 15px 30px
}

.el-message-box .el-message-box__header span {
  font-weight: 700
}

.el-message-box .el-message-box__header .el-message-box__headerbtn {
  right: 30px
}

.el-message-box .el-message-box__header .el-message-box__close {
  color: #777;
  font-size: 18px
}

.el-message-box .el-message-box__header .el-message-box__close:before {
  background: inherit !important;
  color: #777 !important
}

.el-message-box .el-message-box__content {
  padding: 0;
  text-align: center
}

.el-message-box .el-message-box__content .el-message-box__message {
  padding: 0
}

.el-message-box .el-message-box__content .el-message-box__message p {
  text-align: center;
  color: #2a2a2a;
  line-height: 24px
}

.el-message-box .el-message-box__content .img {
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/4f4b9902b4ca4cd18a66978a86bc181b.png) no-repeat;
  background-size: 100% 100%;
  display: block;
  margin-bottom: 5px;
  height: 60px;
  width: 60px;
  position: inherit;
  transform: inherit;
  display: inline-block
}

.el-message--info {
  height: 50px;
  line-height: 50px;
  color: #fff;
  background: #7e7e7c;
  font-size: 12px;
  border-radius: 50px;
  padding: 0 20px;
  top: 50% !important;
  left: 50%;
  transform: translate(-50%, -50%);
  -webkit-transform: translate(-50%, -50%);
  -moz-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  -o-transform: translate(-50%, -50%)
}

.el-message--info .el-icon-info {
  display: none
}

@keyframes showSmallSty {
  0% {
    width: 42px
  }
  to {
    width: 300px
  }
}

@-webkit-keyframes showSmallSty {
  0% {
    width: 42px
  }
  to {
    width: 300px
  }
}

@keyframes showBigSty {
  0% {
    width: 300px
  }
  to {
    width: 42px
  }
}

@-webkit-keyframes showBigSty {
  0% {
    width: 300px
  }
  to {
    width: 42px
  }
}

.swiper {
  position: relative;
  height: 100%;
  width: 100%;
  z-index: 1000000
}

.swiper .close {
  position: fixed;
  top: 20px;
  right: 20px;
  z-index: 20;
  cursor: pointer
}

.swiper .close i {
  font-size: 24px;
  color: #fff
}

.swiper .swiper-mask {
  background: rgba(16, 17, 28, .7);
  z-index: 5
}

.swiper .el-carousel, .swiper .swiper-mask {
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%
}

.swiper .el-carousel {
  z-index: 10
}

.swiper .el-carousel .el-carousel__container {
  height: 100%;
  overflow: hidden
}

.swiper .el-carousel .el-carousel__arrow {
  background-color: rgba(165, 167, 192, .5);
  width: 48px;
  height: 48px
}

.swiper .el-carousel [class*=" el-icon-"], .swiper .el-carousel [class^=el-icon-] {
  color: #3d4059;
  font-size: 20px;
  font-weight: 600
}

.swiper .el-carousel .el-carousel__indicators {
  display: none
}

.swiper .el-carousel .el-carousel__item {
  text-align: center;
  margin-top: calc(50vh - 230px)
}

.swiper .el-carousel .swiper-img {
  max-width: 690px;
  height: 460px;
  -o-object-fit: cover;
  object-fit: cover
}

.swiper .swiper-num {
  position: absolute;
  top: 50%;
  left: 50%;
  font-size: 24px;
  color: #a5a7c0;
  font-family: priceFont;
  margin-top: 240px
}

.swiper .swiper-num span {
  font-size: 32px;
  color: #fff
}

.el-header {
  height: 60px;
  color: #3d4059;
  background: #3d84ff;
  box-shadow: 0 2px 8px 0 rgba(0, 0, 0, .1);
  z-index: 30;
  position: fixed;
  width: 100%;
  padding: 0 62px;
  left: 0
}

.el-header .banner {
  margin: 0 auto;
  min-width: 1200px;
  height: 60px;
  position: relative
}

.el-header .banner .back {
  color: #fff;
  text-decoration: none;
  font-size: 14px;
  line-height: 60px;
  opacity: .75;
  display: inline;
  cursor: pointer
}

.el-header .banner .back:hover {
  opacity: .5
}

.el-header .banner .back:hover i {
  opacity: .75
}

.el-header .banner .back i {
  font-size: 19px;
  color: #fff;
  float: left;
  margin-top: 1px;
  margin-right: 3px
}

.el-header .banner .source-con {
  position: absolute;
  left: 50%;
  text-align: center;
  top: 0;
  transform: translateX(-50%);
  -webkit-transform: translateX(-50%);
  -moz-transform: translateX(-50%);
  -ms-transform: translateX(-50%);
  -o-transform: translateX(-50%);
  margin-top: 10px
}

.el-header .banner .source-con .source-name {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  width: 300px;
  color: #fff;
  font-size: 14px
}

.el-header .banner .source-con .source-down {
  margin-top: 5px;
  display: inline
}

.el-header .banner .source-con .source-down span {
  font-size: 12px;
  color: #fff;
  opacity: .75
}

.el-header .banner .source-con .source-down .source-n {
  margin-right: 10px
}

.el-header .banner .header_userInfo {
  float: right;
  margin: 10px 0 0 30px;
  height: 26px;
  border-radius: 2px;
  line-height: 26px;
  width: 36px;
  position: relative;
  cursor: pointer;
  z-index: 51;
  padding-bottom: 24px
}

.el-header .banner .header_userInfo .userInfo_header {
  float: left;
  margin: 2px;
  height: 32px;
  width: 32px
}

.el-header .banner .header_userInfo .userInfo_header img {
  vertical-align: top;
  border-radius: 100px
}

.el-header .banner .header_userInfo:hover .userLinks {
  display: block
}

.el-header .banner .header_userInfo .userLinks {
  position: absolute;
  z-index: 51;
  display: none;
  width: 120px;
  top: 49px;
  right: 0;
  height: 80px;
  padding: 10px 0;
  background: #fff;
  box-shadow: 0 5px 15px 0 rgba(0, 0, 0, .1);
  border-radius: 2px
}

.el-header .banner .header_userInfo .userLinks li {
  height: 40px;
  line-height: 40px
}

.el-header .banner .header_userInfo .userLinks li:hover {
  background: #ededed
}

.el-header .banner .header_userInfo .userLinks li .userLinks_item {
  font-size: 13px;
  color: #2a2a2a;
  padding: 0 15px;
  display: inline-block
}

.el-header .banner .header_userInfo .userLinks li .userLinks_item .iconfont {
  margin-right: 5px;
  display: inline-block;
  color: #777
}

.el-header .banner .menudivright-r-div {
  float: right
}

.el-header .banner .menudivright-r-div .Patternbtn-div {
  float: left;
  width: 80px;
  text-align: center;
  padding-top: 8px;
  cursor: pointer;
  height: 60px;
  box-sizing: border-box
}

.el-header .banner .menudivright-r-div .Patternbtn-div:hover {
  background: #2b70e6
}

.el-header .banner .menudivright-r-div .Patternbtn-div em {
  font-size: 26px;
  display: inline-block;
  color: #cee0ff
}

.el-header .banner .menudivright-r-div .Patternbtn-div .icon {
  width: 25px;
  height: 25px
}

.el-header .banner .menudivright-r-div .Patternbtn-div p {
  font-size: 12px;
  color: #cee0ff
}

.el-header .banner .menudivright-r-div .morebtn-div {
  width: 80px;
  height: 60px;
  text-align: center;
  position: relative;
  cursor: pointer;
  float: left;
  padding-top: 8px;
  box-sizing: border-box
}

.el-header .banner .menudivright-r-div .morebtn-div:hover {
  background: #2b70e6
}

.el-header .banner .menudivright-r-div .morebtn-div em {
  font-size: 26px;
  display: inline-block;
  color: #cee0ff;
  margin-left: -3px
}

.el-header .banner .menudivright-r-div .morebtn-div p {
  font-size: 12px;
  color: #cee0ff
}

.el-header .banner .menudivright-r-div .morebtn-div:hover .Retirebtn-div {
  display: block
}

.el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div {
  display: none;
  width: 120px;
  height: 40px;
  position: absolute;
  top: 60px;
  left: 0;
  background: #fff;
  line-height: 40px;
  box-shadow: 0 5px 15px 0 rgba(0, 0, 0, .1)
}

.el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div .iconbaizhoumoshi-tuike {
  margin: 3px 0 0 12px;
  display: inline-block;
  color: #d8d8d8;
  width: 25px
}

.el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div span {
  font-size: 13px;
  color: #bfbfbf
}

.el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div:hover span {
  color: #2a2a2a
}

.el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div:hover .iconbaizhoumoshi-tuike {
  color: #bfbfbf
}

.el-header .banner .menudivright-r-div .InformationCenter-div {
  margin-left: 76px;
  margin-right: 30px;
  position: relative
}

.el-header .banner .menudivright-r-div .InformationCenter-div a {
  line-height: 60px;
  font-size: 14px;
  color: #fff;
  opacity: .75;
  cursor: pointer
}

.el-header .banner .menudivright-r-div .InformationCenter-div a:hover {
  opacity: .5
}

.el-header .banner .menudivright-r-div .InformationCenter-div .noticeTips {
  display: inline-block;
  min-width: 18px;
  height: 18px;
  background: #ff8013;
  border-radius: 50%;
  margin-left: 5px;
  color: #fff;
  line-height: 18px;
  text-align: center;
  font-size: 12px;
  position: absolute;
  top: 21px;
  right: -22px
}

.el-header .banner .menudivright-r-div .backold-div {
  font-size: 14px;
  color: #fff;
  opacity: .75;
  cursor: pointer;
  line-height: 60px
}

.el-header .banner .menudivright-r-div .backold-div:hover {
  opacity: .5
}

.el-header .banner .message-reddot {
  text-decoration: none;
  position: absolute;
  top: -6px;
  right: -14px;
  min-width: 14px;
  height: 14px;
  text-align: center;
  line-height: 14px;
  font-size: 12px;
  color: #fff;
  border-radius: 14px;
  background: #e10e01;
  padding: 0 3px !important
}

.dialog-quit .el-dialog {
  width: 400px;
  height: 480px;
  border-radius: 2px
}

.dialog-quit .el-dialog .el-dialog__header {
  padding: 20px 30px;
  padding-bottom: 15px;
  border-bottom: 1px solid #ededed
}

.dialog-quit .el-dialog .el-dialog__title {
  font-weight: 700
}

.dialog-quit .el-dialog .el-dialog__headerbtn {
  right: 30px
}

.dialog-quit .el-dialog .el-dialog__close {
  color: #777;
  font-size: 18px
}

.dialog-quit .el-dialog .el-dialog__body {
  padding: 0
}

.dialog-quit .el-dialog .el-dialog__body .quit-con {
  margin-top: 30px;
  padding: 0 30px
}

.dialog-quit .el-dialog .el-dialog__body .quit-con h2 {
  font-size: 18px;
  color: #2a2a2a;
  margin-bottom: 90px;
  line-height: 30px
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode {
  margin-bottom: 100px
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode p {
  font-size: 14px;
  color: #2a2a2a;
  letter-spacing: .25px;
  line-height: 24px;
  margin-bottom: 10px
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text {
  overflow: hidden;
  clear: both
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text .el-input {
  width: 180px;
  float: left
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text .el-input .el-input__inner {
  width: 180px;
  height: 32px;
  line-height: 32px;
  padding-left: 5px;
  box-sizing: border-box;
  background: #f6f6f6;
  border: 1px solid #ededed;
  border-radius: 2px;
  color: #2a2a2a
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text .el-input .el-input__inner:focus {
  box-shadow: inherit
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text .el-input .el-input__inner::-webkit-input-placeholder {
  font-size: 14px;
  color: #bfbfbf;
  font-weight: 100
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text .el-input .el-input__inner:-moz-placeholder, .dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text .el-input .el-input__inner::-moz-placeholder {
  font-size: 14px;
  color: #bfbfbf;
  font-weight: 100
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text .el-input .el-input__inner:-ms-input-placeholder {
  font-size: 14px;
  color: #bfbfbf;
  font-weight: 100
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text .s-canvas, .dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text img {
  margin: 0 10px;
  height: 32px;
  width: 80px;
  float: left
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .text span {
  float: left;
  line-height: 32px;
  color: #777;
  font-size: 14px;
  cursor: pointer
}

.dialog-quit .el-dialog .el-dialog__body .quit-con .yecode .error-code {
  color: #ff2a24;
  line-height: 24px;
  margin-top: 10px
}

.dialog-quit .el-dialog .el-dialog__body .con-up {
  margin-bottom: 30px
}

.dialog-quit .el-dialog .el-dialog__body .tit {
  font-size: 14px;
  color: #777;
  line-height: 24px;
  margin-bottom: 5px
}

.dialog-quit .el-dialog .el-dialog__body .con {
  font-size: 14px;
  color: #2a2a2a;
  line-height: 24px;
  font-weight: 700
}

.dialog-quit .el-dialog .el-dialog__body textarea {
  margin-bottom: 10px;
  resize: none;
  width: 340px;
  height: 80px;
  padding: 5px 10px;
  box-sizing: border-box;
  background: #f6f6f6;
  border: 1px solid #ededed;
  box-shadow: inset 0 -1px 0 0 #ededed;
  border-radius: 2px;
  color: #2a2a2a
}

.dialog-quit .el-dialog .el-dialog__body textarea::-webkit-input-placeholder {
  font-size: 14px;
  color: #bfbfbf;
  font-weight: 100
}

.dialog-quit .el-dialog .el-dialog__body textarea:-moz-placeholder, .dialog-quit .el-dialog .el-dialog__body textarea::-moz-placeholder {
  font-size: 14px;
  color: #bfbfbf;
  font-weight: 100
}

.dialog-quit .el-dialog .el-dialog__body textarea:-ms-input-placeholder {
  font-size: 14px;
  color: #bfbfbf;
  font-weight: 100
}

.dialog-quit .el-dialog .el-dialog__body .tip {
  font-size: 12px;
  color: #777;
  line-height: 18px
}

.dialog-quit .el-dialog .el-dialog__footer {
  padding: 0;
  text-align: center;
  position: absolute;
  bottom: 20px;
  left: 75px
}

.dialog-quit .el-dialog .el-dialog__footer .btn {
  background: #3d84ff;
  width: 120px;
  height: 40px;
  text-align: center;
  color: #fff;
  border: 1px solid #3d84ff;
  border-radius: 0
}

.dialog-quit .el-dialog .el-dialog__footer .btn:hover {
  background: rgba(61, 132, 255, .8)
}

.dialog-quit .el-dialog .el-dialog__footer .cancel {
  background: #fff;
  border: 1px solid #ededed;
  color: #2a2a2a
}

.dialog-quit .el-dialog .el-dialog__footer .cancel:hover {
  background: #ededed
}

.black .el-header {
  background: #2a2a2a
}

.black .el-header .banner .back {
  color: #777;
  opacity: inherit
}

.black .el-header .banner .back:hover, .black .el-header .banner .back:hover i {
  color: #bfbfbf;
  opacity: inherit
}

.black .el-header .banner .back i {
  color: #777
}

.black .el-header .banner .source-con .source-name {
  color: #bfbfbf
}

.black .el-header .banner .source-con .source-down span {
  color: #777;
  opacity: inherit
}

.black .el-header .banner .header_userInfo .userLinks {
  background: #2a2a2a;
  box-shadow: 0 5px 15px 0 rgba(0, 0, 0, .1)
}

.black .el-header .banner .header_userInfo .userLinks li:hover {
  background: #3f3f3f
}

.black .el-header .banner .header_userInfo .userLinks li .userLinks_item {
  color: #777
}

.black .el-header .banner .header_userInfo .userLinks li .userLinks_item:hover, .black .el-header .banner .header_userInfo .userLinks li .userLinks_item:hover .iconfont {
  color: #bfbfbf
}

.black .el-header .banner .menudivright-r-div .Patternbtn-div:hover {
  background: #1d1d1d
}

.black .el-header .banner .menudivright-r-div .Patternbtn-div em, .black .el-header .banner .menudivright-r-div .Patternbtn-div p {
  color: #777
}

.black .el-header .banner .menudivright-r-div .morebtn-div:hover {
  background: #1d1d1d
}

.black .el-header .banner .menudivright-r-div .morebtn-div em, .black .el-header .banner .menudivright-r-div .morebtn-div p {
  color: #777
}

.black .el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div {
  background: #2a2a2a;
  box-shadow: 0 5px 15px 0 rgba(0, 0, 0, .1)
}

.black .el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div .iconbaizhoumoshi-tuike, .black .el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div span {
  color: #3f3f3f
}

.black .el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div:hover .iconbaizhoumoshi-tuike, .black .el-header .banner .menudivright-r-div .morebtn-div .Retirebtn-div:hover span {
  color: #bfbfbf
}

.black .el-header .banner .menudivright-r-div .InformationCenter-div a {
  color: #777;
  opacity: inherit
}

.black .el-header .banner .menudivright-r-div .InformationCenter-div a:hover {
  opacity: inherit;
  color: #bfbfbf
}

.black .el-header .banner .menudivright-r-div .InformationCenter-div .noticeTips {
  background: #ff8013;
  color: #fff
}

.black .el-header .banner .menudivright-r-div .InformationCenter-div .noticeTips:hover {
  opacity: inherit;
  color: #fff
}

.black .el-header .banner .menudivright-r-div .backold-div {
  color: #777;
  opacity: inherit
}

.black .el-header .banner .menudivright-r-div .backold-div:hover {
  opacity: inherit;
  color: #bfbfbf
}

.exploreTip {
  height: 52px;
  background-color: #fbbf30;
  width: 100%;
  text-align: center;
  line-height: 52px;
  font-size: 16px;
  position: relative;
  z-index: 33;
  border-bottom: 1px solid #ccc;
  font-family: Microsoft Yahei
}

.exploreTip div {
  color: #a77600
}

.exploreTip div .browser-download {
  position: relative;
  cursor: pointer;
  color: #fff
}

.exploreTip div .browser-download .browser-version-list {
  position: absolute;
  top: 20px;
  left: 50%;
  margin-left: -48px;
  display: none
}

.exploreTip div .browser-download .browser-version-list li {
  width: 96px;
  height: 40px
}

.exploreTip div .browser-download .browser-version-list li a {
  display: block;
  background: #000;
  line-height: 40px;
  text-decoration: none;
  font-size: 14px
}

.exploreTip div .browser-download .browser-version-list .arrow {
  width: 16px;
  height: 8px;
  margin-left: 40px;
  background: url(//image.zhihuishu.com/testzhs/ablecommons/demo/201704/0b241b0%E2%80%A6.png) no-repeat
}

.exploreTip .hint_delete {
  position: absolute;
  top: 0;
  right: 40px
}

.exploreTip .hint_delete a {
  display: block;
  width: 78px;
  height: 26px;
  margin-top: 13px;
  font-size: 14px;
  text-decoration: none;
  color: #fbbf30;
  text-align: center;
  line-height: 26px;
  background: #fff;
  border-radius: 13px
}

.dialog-abnormal-behavior p[data-v-20d74199] {
  font-family: PingFangSC-Semibold;
  font-size: 17px;
  color: #111;
  text-align: center
}

.dialog-abnormal-behavior .footer[data-v-20d74199] {
  margin-top: 30px;
  display: flex;
  align-items: center;
  justify-content: center
}

.dialog-abnormal-behavior .footer .s1[data-v-20d74199] {
  margin-right: 20px;
  width: 134px;
  height: 44px;
  text-align: center;
  line-height: 44px;
  background: #fff;
  border: 1px solid #ededed;
  border-radius: 8px;
  font-size: 17px;
  color: #2a2a2a;
  font-family: PingFangSC-Regular
}

.dialog-abnormal-behavior .footer[data-v-20d74199] :hover {
  cursor: pointer
}

.dialog-abnormal-behavior .footer .s2[data-v-20d74199] {
  width: 134px;
  height: 44px;
  text-align: center;
  line-height: 44px;
  background: #5d82ff;
  border-radius: 8px;
  font-size: 17px;
  color: #fff;
  font-family: PingFangSC-Regular
}

.dialog-abnormal-behavior .footer .s2[data-v-20d74199] :hover {
  cursor: pointer
}

.el-dialog .el-dialog__header {
  display: flex;
  align-items: center
}

.dialog-abnormal-behavior[data-v-33d7c538] {
  border-radius: 16px
}

.dialog-abnormal-behavior .el-dialog__body[data-v-33d7c538] {
  padding: 20px
}

.dialog-abnormal-behavior .header-title[data-v-33d7c538] {
  line-height: 24px;
  clear: both;
  zoom: 1;
  height: 24px
}

.dialog-abnormal-behavior .header-title i[data-v-33d7c538] {
  float: right;
  font-size: 16px;
  cursor: pointer
}

.dialog-abnormal-behavior .header-title span[data-v-33d7c538] {
  float: left;
  font-size: 17px;
  color: #111;
  line-height: 24px
}

.dialog-abnormal-behavior .main-box[data-v-33d7c538] {
  padding: 0 20px
}

.dialog-abnormal-behavior .main-box .tips[data-v-33d7c538] {
  font-size: 17px;
  color: #111
}

.dialog-abnormal-behavior .main-box .form-box[data-v-33d7c538] {
  padding: 30px 0;
  width: 320px;
  margin: 0 auto
}

.dialog-abnormal-behavior .main-box .from-item[data-v-33d7c538] {
  height: 70px;
  clear: both;
  overflow: hidden
}

.dialog-abnormal-behavior .main-box .from-item .input-sty[data-v-33d7c538] {
  display: block;
  float: left;
  width: 180px;
  height: 40px;
  background: #eeeef5;
  border-radius: 8px;
  border: none;
  padding: 0 15px;
  color: #111;
  font-size: 14px
}

.dialog-abnormal-behavior .main-box .from-item .code-imgage[data-v-33d7c538], .dialog-abnormal-behavior .main-box .from-item .message-btn[data-v-33d7c538] {
  display: block;
  width: 100px;
  height: 40px;
  float: right;
  border-radius: 8px;
  border: none
}

.dialog-abnormal-behavior .main-box .from-item .message-btn[data-v-33d7c538] {
  color: #fff
}

.dialog-abnormal-behavior .main-box .submit-btn[data-v-33d7c538] {
  width: 120px;
  height: 44px;
  display: block;
  margin: 0 auto;
  font-size: 17px;
  border-radius: 8px;
  color: #fff;
  border: none
}

.dialog-abnormal-behavior .main-box .active-color[data-v-33d7c538] {
  background: #5d82ff;
  cursor: pointer
}

.dialog-abnormal-behavior .main-box .wait-color[data-v-33d7c538] {
  background: #6f7bb2;
  cursor: not-allowed
}

.dialog-abnormal-behavior .main-box .disable-color[data-v-33d7c538] {
  background: #ccc;
  cursor: not-allowed
}

.video-study {
  height: 100%;
  overflow: hidden
}

.video-study .box-content {
  margin-top: 60px;
  position: relative;
  height: 100%;
  min-width: 1200px
}

.video-study .box-content .box-left {
  width: calc(100% - 340px);
  height: 100%;
  background: #000;
  position: relative
}

.video-study .box-content .box-left .left-top {
  background: #f6f6f6;
  box-shadow: inset -1px 0 0 0 #ededed;
  right: 340px;
  height: 40px;
  line-height: 40px;
  position: absolute;
  left: 0;
  top: 0;
  padding: 0 35px 0 60px;
  z-index: 2;
  width: 100%;
  box-sizing: border-box
}

.video-study .box-content .box-left .left-top .videotop_lesson {
  text-align: right
}

.video-study .box-content .box-left .left-top .videotop_lesson, .video-study .box-content .box-left .left-top .videotop_lesson_tit {
  height: 40px;
  line-height: 40px;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  display: inline-block;
  font-size: 12px;
  color: #2a2a2a
}

.video-study .box-content .box-left .left-top .videotop_lesson_tit {
  max-width: 400px;
  margin-left: 5px
}

.video-study .box-content .box-left .left-top .videotop_all ul li {
  float: left;
  margin: 6px 5px 0 0;
  cursor: pointer;
  list-style: none;
  height: 30px;
  line-height: 30px;
  font-size: 12px;
  text-align: right;
  padding-left: 14px;
  padding-right: 10px
}

.video-study .box-content .box-left .left-top .videotop_all ul li em {
  margin-top: 0;
  margin-right: 3px;
  color: #d8d8d8
}

.video-study .box-content .box-left .left-top .videotop_all ul li span {
  color: #777
}

.video-study .box-content .box-left .left-top .videotop_all ul li:hover span {
  color: #2a2a2a
}

.video-study .box-content .box-left .limitInfo {
  position: absolute;
  transform: translate(-50%, -50%);
  -webkit-transform: translate(-50%, -50%);
  -moz-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  -o-transform: translate(-50%, -50%);
  background: rgba(42, 42, 42, .95);
  border-radius: 30px;
  width: 630px;
  top: 50%;
  left: 50%;
  box-sizing: border-box
}

.video-study .box-content .box-left .limitInfo .title {
  line-height: 30px;
  color: #ededed;
  font-size: 18px;
  text-align: center;
  margin-top: 30px
}

.video-study .box-content .box-left .limitInfo .limit-tips {
  line-height: 20px;
  margin-top: 20px;
  color: #bfbfbf;
  font-size: 14px;
  text-align: center
}

.video-study .box-content .box-left .limitInfo ul {
  margin-top: 5px;
  margin-bottom: 20px
}

.video-study .box-content .box-left .limitInfo ul li {
  line-height: 48px;
  color: #fff;
  font-size: 24px;
  text-align: center
}

.video-study .box-content .box-left .threed-box {
  position: absolute;
  bottom: 120px;
  left: 40px;
  height: 32px;
  background: hsla(0, 0%, 100%, .9);
  border-radius: 21px;
  width: 32px;
  overflow: hidden;
  clear: both;
  transition: .5s;
  cursor: pointer;
  z-index: 2
}

.video-study .box-content .box-left .threed-box .icon {
  width: 24px;
  height: 24px;
  float: left;
  border: 4px solid #fff;
  margin-right: 5px;
  border-radius: 50px
}

.video-study .box-content .box-left .threed-box span {
  margin: 0 5px;
  font-size: 14px;
  line-height: 32px;
  color: #666;
  max-width: 145px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  display: block;
  float: left
}

.video-study .box-content .box-left .threed-box .iconfont {
  font-size: 20px;
  transform: rotateY(180deg);
  float: right;
  color: #666;
  margin-right: 8px;
  margin-top: 5px
}

.video-study .box-content .box-left .three-show {
  width: 220px
}

.video-study .box-content .box-left .video-topic {
  position: absolute;
  bottom: 10px;
  width: 100%;
  height: 20px;
  right: 5px;
  z-index: 2
}

.video-study .box-content .box-left .video-topic ul {
  margin-right: 10px
}

.video-study .box-content .box-left .video-topic ul li {
  cursor: pointer;
  background: #fff;
  width: 5px;
  height: 5px;
  border-radius: 5px;
  position: absolute
}

.video-study .box-content .box-left .video-topic ul li span {
  display: block;
  width: 100%;
  height: 5px;
  position: relative
}

.video-study .box-content .box-left .video-topic ul li span .el-popover {
  left: 0;
  bottom: 10px
}

.video-study .box-content .box-right {
  position: absolute;
  height: 100%;
  top: 0;
  bottom: 0;
  right: 0;
  width: 340px
}

.video-study .box-content .box-right .newListTest {
  padding: 0 15px;
  overflow: hidden;
  clear: both
}

.video-study .box-content .box-right .newListTest li {
  margin-right: 5px;
  height: 80px;
  list-style: none;
  float: left;
  width: 100px;
  text-align: center;
  line-height: 30px;
  font-size: 12px;
  color: #bfbfbf;
  cursor: pointer
}

.video-study .box-content .box-right .newListTest li:nth-child(3n) {
  margin-right: 0
}

.video-study .box-content .box-right .newListTest li:hover {
  background: #ededed
}

.video-study .box-content .box-right .newListTest li a {
  font-size: 12px;
  color: #777;
  display: inline-block;
  line-height: 19px;
  margin-top: 10px
}

.video-study .box-content .box-right .newListTest li a .icon {
  width: 40px;
  height: 40px
}

.video-study .box-content .box-right .topicTitle {
  width: 340px;
  height: 40px;
  background: #f6f6f6
}

.video-study .box-content .box-right .topicTitle ul {
  margin-left: 20px
}

.video-study .box-content .box-right .topicTitle ul .tabTitle {
  font-size: 14px;
  color: #2a2a2a;
  line-height: 40px
}

.video-study .box-content .box-right .list {
  position: relative;
  padding-bottom: 20px;
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/892e66724a934d7291452c71a992f244.png) 68px 0 repeat-y
}

.video-study .box-content .box-right .list .position_first_bg {
  position: absolute;
  z-index: 1;
  left: 68px;
  top: -11px;
  display: inline-block;
  height: 20px;
  width: 2px
}

.video-study .box-content .box-right .list li {
  position: relative;
  padding: 7px 10px 7px 3px !important;
  height: 36px;
  font-family: Tahoma;
  width: 100%;
  font-size: 12px
}

.video-study .box-content .box-right .list li:hover {
  background: #ededed;
  font-size: 12px;
  color: #2a2a2a
}

.video-study .box-content .box-right .list li:hover .chapter-em {
  background: url(https://image.zhihuishu.com/zhs_yufa_150820/ablecommons/demo/201910/2644659e82f34d9ea62a0f436f0ac1e9.png) no-repeat
}

.video-study .box-content .box-right .list li .catalogue_title3 {
  font-size: 12px;
  color: #777;
  line-height: 38px;
  height: 26px;
  display: inline-block;
  text-align: right;
  width: 50px;
  padding-right: 7px;
  overflow: hidden
}

.video-study .box-content .box-right .list li .catalogue_title4 {
  font-size: 12px;
  color: #999;
  line-height: 38px;
  height: 26px;
  display: inline-block;
  text-align: right;
  width: 50px;
  padding-right: 7px;
  overflow: hidden
}

.video-study .box-content .box-right .list li .cataloguediv-l {
  width: 50px;
  padding-right: 18px
}

.video-study .box-content .box-right .list li .time_ico_box {
  display: block;
  height: 20px;
  margin-left: 1px;
  margin-right: 14px
}

.video-study .box-content .box-right .list li .catalogue_title {
  font-size: 12px;
  color: #2a2a2a;
  margin-bottom: 5px;
  line-height: 18px;
  display: block;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  width: 200px
}

.video-study .box-content .box-right .list li .small-lesson {
  line-height: 36px
}

.video-study .box-content .box-right .list li .cataloguediv-c {
  width: 210px;
  margin-left: 20px
}

.video-study .box-content .box-right .list li .time_ico_half {
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/5efaa4c4040e4042bde4fc1fa61a8e10.png) no-repeat;
  display: inline-block;
  height: 12px;
  margin: 1px 5px 0 0;
  width: 12px
}

.video-study .box-content .box-right .list li .time_icofinish {
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/5b3134c2c263451c8d45cb477b5f79e4.png) no-repeat;
  position: absolute;
  right: 24px;
  top: 17px;
  width: 17px;
  height: 17px;
  display: block
}

.video-study .box-content .box-right .list li .el-progress {
  position: absolute;
  right: 25px;
  top: 10px
}

.video-study .box-content .box-right .list li .el-progress .el-progress-circle {
  height: 16px !important;
  width: 16px !important
}

.video-study .box-content .box-right .list li .el-progress .el-progress__text {
  font-size: 12px !important;
  color: #3d84ff
}

.video-study .box-content .box-right .list li .el-progress .el-progress-circle__track {
  stroke: #3d84ff;
  opacity: .3
}

.video-study .box-content .box-right .list li .el-progress .el-progress-circle__path {
  stroke: #3d84ff
}

.video-study .box-content .box-right .list li .progress-num {
  position: absolute;
  right: 20px;
  top: 28px;
  font-size: 12px !important;
  color: #3d84ff
}

.video-study .box-content .box-right .list li .time {
  color: #777;
  font-size: 12px
}

.video-study .box-content .box-right .list li .learningPercentage-div {
  width: 20px;
  height: 20px;
  position: relative;
  right: 14px
}

.video-study .box-content .box-right .list li .learningPercentage-div .learningPercentage-span {
  position: absolute;
  bottom: -16px;
  left: 0;
  font-size: 12px;
  color: #3d84ff
}

.video-study .box-content .box-right .list li .learningPercentage-div .progressCricle {
  width: 20px;
  height: 20px
}

.video-study .box-content .box-right .list li .Sectionmark-em {
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/5e635034f9e24ab48c97fc7fcf1b516a.png) no-repeat;
  width: 11px;
  height: 11px;
  display: inline-block;
  position: absolute;
  left: 64px;
  top: 20px
}

.video-study .box-content .box-right .list .chapter-test {
  padding-left: 61px !important;
  cursor: pointer;
  line-height: 40px;
  line-height: 37px;
  color: #2a2a2a;
  position: relative
}

.video-study .box-content .box-right .list .chapter-test .name {
  margin-left: 30px;
  color: #2a2a2a;
  font-size: 12px
}

.video-study .box-content .box-right .list .chapter-test .iconfont {
  padding: 0 20px;
  cursor: pointer;
  position: absolute;
  right: 62px;
  top: 8px;
  color: #666
}

.video-study .box-content .box-right .list .chapter-test .finish {
  height: 17px;
  width: 17px;
  display: block;
  cursor: pointer;
  position: absolute;
  right: 82px;
  top: 17px;
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/5b3134c2c263451c8d45cb477b5f79e4.png) no-repeat
}

.video-study .box-content .box-right .list .video {
  cursor: pointer
}

.video-study .box-content .box-right .list .font_gray_inclined .catalogue_title {
  margin-top: 10px;
  font-size: 14px;
  font-weight: 700
}

.video-study .box-content .box-right .list .font_gray_inclined .chapter-em {
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/7943740388164e14980b89c244f35c58.png) no-repeat;
  width: 11px;
  height: 11px;
  display: inline-block;
  margin: 13px 0 0 3px
}

.video-study .box-content .box-right .list .current_play {
  background: rgba(61, 132, 255, .15)
}

.video-study .box-content .box-right .list .current_play .catalogue_title3, .video-study .box-content .box-right .list .current_play .catalogue_title4 {
  color: #3d84ff
}

.video-study .box-content .box-right .list .current_play .catalogue_title {
  color: #3d84ff;
  font-weight: 700
}

.video-study .box-content .box-right .list .current_play .time_ico_half {
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/51172bf9b834437492667911fb2a6b68.png) no-repeat
}

.video-study .box-content .box-right .list .current_play .time {
  font-size: 12px;
  color: rgba(61, 132, 255, .8);
  letter-spacing: .1px
}

.video-study .el-scrollbar .el-scrollbar__wrap {
  overflow-x: hidden
}

.video-study .el-scrollbar .el-scrollbar__bar {
  right: 0
}

.video-study .el-scrollbar .is-horizontal {
  opacity: 0 !important;
  display: none
}

.video-study .el-scrollbar .el-scrollbar__thumb {
  background: #bfbfbf;
  width: 4px
}

.video-study .dialog-aberrant .el-dialog, .video-study .dialog-back .el-dialog, .video-study .dialog-class .el-dialog, .video-study .dialog-img .el-dialog, .video-study .dialog-look-ans .el-dialog, .video-study .dialog-read .el-dialog, .video-study .dialog-teach .el-dialog, .video-study .dialog-test .el-dialog, .video-study .dialog-tips .el-dialog, .video-study .dialog-warn .el-dialog, .video-study .read-learn .el-dialog {
  width: 400px;
  height: 250px;
  border-radius: 2px
}

.video-study .dialog-aberrant .el-dialog .el-dialog__header, .video-study .dialog-back .el-dialog .el-dialog__header, .video-study .dialog-class .el-dialog .el-dialog__header, .video-study .dialog-img .el-dialog .el-dialog__header, .video-study .dialog-look-ans .el-dialog .el-dialog__header, .video-study .dialog-read .el-dialog .el-dialog__header, .video-study .dialog-teach .el-dialog .el-dialog__header, .video-study .dialog-test .el-dialog .el-dialog__header, .video-study .dialog-tips .el-dialog .el-dialog__header, .video-study .dialog-warn .el-dialog .el-dialog__header, .video-study .read-learn .el-dialog .el-dialog__header {
  padding: 20px 30px;
  padding-bottom: 15px
}

.video-study .dialog-aberrant .el-dialog .el-dialog__title, .video-study .dialog-back .el-dialog .el-dialog__title, .video-study .dialog-class .el-dialog .el-dialog__title, .video-study .dialog-img .el-dialog .el-dialog__title, .video-study .dialog-look-ans .el-dialog .el-dialog__title, .video-study .dialog-read .el-dialog .el-dialog__title, .video-study .dialog-teach .el-dialog .el-dialog__title, .video-study .dialog-test .el-dialog .el-dialog__title, .video-study .dialog-tips .el-dialog .el-dialog__title, .video-study .dialog-warn .el-dialog .el-dialog__title, .video-study .read-learn .el-dialog .el-dialog__title {
  font-weight: 700
}

.video-study .dialog-aberrant .el-dialog .el-dialog__headerbtn, .video-study .dialog-back .el-dialog .el-dialog__headerbtn, .video-study .dialog-class .el-dialog .el-dialog__headerbtn, .video-study .dialog-img .el-dialog .el-dialog__headerbtn, .video-study .dialog-look-ans .el-dialog .el-dialog__headerbtn, .video-study .dialog-read .el-dialog .el-dialog__headerbtn, .video-study .dialog-teach .el-dialog .el-dialog__headerbtn, .video-study .dialog-test .el-dialog .el-dialog__headerbtn, .video-study .dialog-tips .el-dialog .el-dialog__headerbtn, .video-study .dialog-warn .el-dialog .el-dialog__headerbtn, .video-study .read-learn .el-dialog .el-dialog__headerbtn {
  right: 30px
}

.video-study .dialog-aberrant .el-dialog .el-dialog__close, .video-study .dialog-back .el-dialog .el-dialog__close, .video-study .dialog-class .el-dialog .el-dialog__close, .video-study .dialog-img .el-dialog .el-dialog__close, .video-study .dialog-look-ans .el-dialog .el-dialog__close, .video-study .dialog-read .el-dialog .el-dialog__close, .video-study .dialog-teach .el-dialog .el-dialog__close, .video-study .dialog-test .el-dialog .el-dialog__close, .video-study .dialog-tips .el-dialog .el-dialog__close, .video-study .dialog-warn .el-dialog .el-dialog__close, .video-study .read-learn .el-dialog .el-dialog__close {
  color: #777;
  font-size: 18px
}

.video-study .dialog-aberrant .el-dialog .el-dialog__body, .video-study .dialog-back .el-dialog .el-dialog__body, .video-study .dialog-class .el-dialog .el-dialog__body, .video-study .dialog-img .el-dialog .el-dialog__body, .video-study .dialog-look-ans .el-dialog .el-dialog__body, .video-study .dialog-read .el-dialog .el-dialog__body, .video-study .dialog-teach .el-dialog .el-dialog__body, .video-study .dialog-test .el-dialog .el-dialog__body, .video-study .dialog-tips .el-dialog .el-dialog__body, .video-study .dialog-warn .el-dialog .el-dialog__body, .video-study .read-learn .el-dialog .el-dialog__body {
  padding: 0 64px;
  text-align: center
}

.video-study .dialog-aberrant .el-dialog .el-dialog__body img, .video-study .dialog-back .el-dialog .el-dialog__body img, .video-study .dialog-class .el-dialog .el-dialog__body img, .video-study .dialog-img .el-dialog .el-dialog__body img, .video-study .dialog-look-ans .el-dialog .el-dialog__body img, .video-study .dialog-read .el-dialog .el-dialog__body img, .video-study .dialog-teach .el-dialog .el-dialog__body img, .video-study .dialog-test .el-dialog .el-dialog__body img, .video-study .dialog-tips .el-dialog .el-dialog__body img, .video-study .dialog-warn .el-dialog .el-dialog__body img, .video-study .read-learn .el-dialog .el-dialog__body img {
  margin-bottom: 5px
}

.video-study .dialog-aberrant .el-dialog .el-dialog__body p, .video-study .dialog-back .el-dialog .el-dialog__body p, .video-study .dialog-class .el-dialog .el-dialog__body p, .video-study .dialog-img .el-dialog .el-dialog__body p, .video-study .dialog-look-ans .el-dialog .el-dialog__body p, .video-study .dialog-read .el-dialog .el-dialog__body p, .video-study .dialog-teach .el-dialog .el-dialog__body p, .video-study .dialog-test .el-dialog .el-dialog__body p, .video-study .dialog-tips .el-dialog .el-dialog__body p, .video-study .dialog-warn .el-dialog .el-dialog__body p, .video-study .read-learn .el-dialog .el-dialog__body p {
  font-size: 14px;
  color: #2a2a2a;
  line-height: 24px
}

.video-study .dialog-aberrant .el-dialog .el-dialog__footer, .video-study .dialog-back .el-dialog .el-dialog__footer, .video-study .dialog-class .el-dialog .el-dialog__footer, .video-study .dialog-img .el-dialog .el-dialog__footer, .video-study .dialog-look-ans .el-dialog .el-dialog__footer, .video-study .dialog-read .el-dialog .el-dialog__footer, .video-study .dialog-teach .el-dialog .el-dialog__footer, .video-study .dialog-test .el-dialog .el-dialog__footer, .video-study .dialog-tips .el-dialog .el-dialog__footer, .video-study .dialog-warn .el-dialog .el-dialog__footer, .video-study .read-learn .el-dialog .el-dialog__footer {
  padding: 0;
  text-align: center;
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  -webkit-transform: translateX(-50%);
  -moz-transform: translateX(-50%);
  -ms-transform: translateX(-50%);
  -o-transform: translateX(-50%)
}

.video-study .dialog-aberrant .el-dialog .el-dialog__footer .btn, .video-study .dialog-back .el-dialog .el-dialog__footer .btn, .video-study .dialog-class .el-dialog .el-dialog__footer .btn, .video-study .dialog-img .el-dialog .el-dialog__footer .btn, .video-study .dialog-look-ans .el-dialog .el-dialog__footer .btn, .video-study .dialog-read .el-dialog .el-dialog__footer .btn, .video-study .dialog-teach .el-dialog .el-dialog__footer .btn, .video-study .dialog-test .el-dialog .el-dialog__footer .btn, .video-study .dialog-tips .el-dialog .el-dialog__footer .btn, .video-study .dialog-warn .el-dialog .el-dialog__footer .btn, .video-study .read-learn .el-dialog .el-dialog__footer .btn {
  background: #3d84ff;
  width: 120px;
  height: 40px;
  text-align: center;
  color: #fff;
  border: 0;
  border-radius: 0
}

.video-study .dialog-aberrant .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-back .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-class .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-img .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-look-ans .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-read .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-teach .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-test .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-tips .el-dialog .el-dialog__footer .btn:hover, .video-study .dialog-warn .el-dialog .el-dialog__footer .btn:hover, .video-study .read-learn .el-dialog .el-dialog__footer .btn:hover {
  background: rgba(61, 132, 255, .8)
}

.video-study .dialog-tips .el-dialog .el-dialog__body {
  padding: 0 26px
}

.video-study .dialog-aberrant .el-dialog {
  height: 300px
}

.video-study .dialog-aberrant .el-dialog .el-dialog__body {
  padding: 0 26px
}

.video-study .dialog-back .el-dialog .el-dialog__body {
  margin-top: 20px;
  padding: 0 35px;
  text-align: left
}

.video-study .dialog-back .el-dialog .el-dialog__body p {
  font-size: 16px;
  color: #2a2a2a;
  line-height: 24px
}

.video-study .aberrant {
  position: absolute;
  transform: translate(-50%, -50%);
  -webkit-transform: translate(-50%, -50%);
  -moz-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  -o-transform: translate(-50%, -50%);
  background: rgba(42, 42, 42, .95);
  border-radius: 30px;
  width: 630px;
  top: 50%;
  left: 50%;
  box-sizing: border-box;
  z-index: 101
}

.video-study .aberrant .title {
  line-height: 30px;
  color: #ededed;
  font-size: 18px;
  text-align: center;
  margin-top: 30px;
  padding: 0 40px
}

.video-study .aberrant .limit-tips {
  line-height: 20px;
  margin-top: 20px;
  color: #bfbfbf;
  font-size: 14px;
  text-align: center
}

.video-study .aberrant ul {
  margin-top: 5px;
  margin-bottom: 20px
}

.video-study .aberrant ul li {
  line-height: 48px;
  color: #fff;
  font-size: 24px;
  text-align: center
}

.video-study .aberrant a {
  display: block;
  background: #3d84ff;
  width: 120px;
  height: 40px;
  text-align: center;
  color: #fff;
  border: 0;
  border-radius: 0;
  margin: 0 auto;
  margin-bottom: 20px;
  line-height: 40px;
  cursor: pointer;
  z-index: 20
}

.video-study .dialog-teach .el-dialog, .video-study .dialog-test .el-dialog, .video-study .dialog-warn .el-dialog {
  height: 480px;
  width: 630px
}

.video-study .dialog-teach .el-dialog .el-dialog__body, .video-study .dialog-test .el-dialog .el-dialog__body, .video-study .dialog-warn .el-dialog .el-dialog__body {
  padding: 0 90px;
  text-align: center;
  margin-top: 30px
}

.video-study .dialog-teach .el-dialog .el-dialog__body p, .video-study .dialog-test .el-dialog .el-dialog__body p, .video-study .dialog-warn .el-dialog .el-dialog__body p {
  font-size: 14px;
  color: #2a2a2a;
  line-height: 24px;
  text-align: left
}

.video-study .dialog-teach .el-dialog .el-dialog__body {
  padding: 0;
  text-align: left;
  margin-top: 30px
}

.video-study .dialog-teach .el-dialog .el-dialog__body h2 {
  text-align: center;
  line-height: 30px;
  font-size: 18px;
  color: #2a2a2a;
  margin-bottom: 20px
}

.video-study .dialog-teach .el-dialog .el-dialog__body h3 {
  text-align: left;
  line-height: 20px;
  font-size: 14px;
  color: #2a2a2a
}

.video-study .dialog-teach .el-dialog .el-dialog__body .teach-box {
  padding: 0 90px
}

.video-study .dialog-teach .el-dialog .el-dialog__body ul li p {
  margin: 12px 0;
  font-size: 14px;
  color: #2a2a2a;
  line-height: 24px;
  text-align: left;
  word-wrap: break-word
}

.video-study .dialog-test .el-dialog .el-dialog__header {
  border-bottom: 1px solid #ededed
}

.video-study .dialog-test .el-dialog .el-dialog__header h4 {
  font-size: 18px;
  color: #2a2a2a;
  line-height: 30px
}

.video-study .dialog-test .el-dialog .el-dialog__header p {
  font-size: 12px;
  color: #777;
  position: relative;
  line-height: 18px
}

.video-study .dialog-test .el-dialog .el-dialog__body {
  margin-top: 0;
  padding: 0
}

.video-study .dialog-test .el-dialog .el-scrollbar__wrap {
  padding-top: 30px
}

.video-study .dialog-test .el-dialog .radio {
  margin: 0 90px;
  margin-bottom: 90px
}

.video-study .dialog-test .el-dialog .topic-title {
  font-size: 14px;
  line-height: 24px;
  color: #333;
  margin-bottom: 10px;
  position: relative
}

.video-study .dialog-test .el-dialog .topic-title .title-tit {
  color: #151515;
  font-weight: 600
}

.video-study .dialog-test .el-dialog .topic-title img {
  max-width: 100%;
  height: auto !important;
  -o-object-fit: cover;
  object-fit: cover;
  vertical-align: middle
}

.video-study .dialog-test .el-dialog .topic-title .error, .video-study .dialog-test .el-dialog .topic-title .right {
  color: #00d789;
  margin-right: 12px;
  position: absolute;
  left: -48px
}

.video-study .dialog-test .el-dialog .topic-title .error .iconfont, .video-study .dialog-test .el-dialog .topic-title .right .iconfont {
  font-size: 14px;
  position: absolute;
  left: -20px
}

.video-study .dialog-test .el-dialog .topic-title .error {
  color: #f94f17
}

.video-study .dialog-test .el-dialog .topic-list {
  margin-left: 0;
  list-style: none
}

.video-study .dialog-test .el-dialog .topic-list .topic-item {
  font-size: 14px;
  color: #2a2a2a;
  padding: 13px 20px 13px 60px;
  position: relative;
  line-height: 24px;
  word-break: break-all;
  cursor: pointer
}

.video-study .dialog-test .el-dialog .topic-list .topic-item .topic-option {
  position: absolute;
  top: 50%;
  margin-top: -9px;
  width: 18px;
  height: 18px;
  text-align: center;
  left: 15px
}

.video-study .dialog-test .el-dialog .topic-list .topic-item .topic-option-item {
  position: absolute;
  top: 50%;
  margin-top: -12px;
  text-align: center;
  left: 40px;
  color: #2a2a2a;
  font-size: 14px
}

.video-study .dialog-test .el-dialog .topic-list .topic-item .active, .video-study .dialog-test .el-dialog .topic-list .topic-item .iconxuanzhong {
  color: #3d84ff
}

.video-study .dialog-test .el-dialog .topic-list .topic-item .item-topic {
  text-align: left
}

.video-study .dialog-test .el-dialog .topic-list .topic-item .item-topic p {
  display: inline-block
}

.video-study .dialog-test .el-dialog .topic-list .topic-item .item-topic img {
  max-width: 100%;
  height: auto !important;
  -o-object-fit: cover;
  object-fit: cover;
  vertical-align: middle
}

.video-study .dialog-test .el-dialog .answer-tit {
  margin-top: 13px;
  margin-bottom: 26px;
  font-size: 14px;
  color: #2a2a2a;
  font-weight: 600
}

.video-study .dialog-test .el-dialog .answer {
  margin-bottom: 28px;
  font-size: 14px;
  color: #2a2a2a
}

.video-study .dialog-test .el-dialog .answer span {
  color: #3d84ff
}

.video-study .dialog-test .el-dialog .answer-ans {
  font-size: 14px;
  color: #2a2a2a;
  text-align: left
}

.video-study .dialog-test .el-dialog .answer-ans ul {
  width: 535px
}

.video-study .dialog-test .el-dialog .answer-ans ul li {
  float: left;
  margin-right: 15px
}

.video-study .dialog-test .el-dialog .answer-ans ul li img {
  background-size: cover;
  width: 120px;
  height: 120px
}

.video-study .dialog-test .el-dialog .el-dialog__footer .dialog-footer .btn {
  height: 22px;
  line-height: 22px;
  color: #3d4059;
  border-radius: 12px;
  border: 1px solid #d8d8d8;
  background: #fff;
  font-size: 14px;
  width: 100px;
  cursor: pointer
}

.video-study .dialog-img .el-dialog {
  height: 480px;
  width: 630px
}

.video-study .dialog-img .el-dialog .el-dialog__body {
  padding: 0 30px;
  text-align: center;
  margin-top: 10px;
  height: 360px
}

.video-study .dialog-img .el-dialog .el-dialog__body img {
  -o-object-fit: cover;
  object-fit: cover;
  max-width: 570px;
  height: 100%
}

.video-study .read-learn .el-dialog {
  height: 300px;
  width: 440px
}

.video-study .read-learn .el-dialog .el-dialog__body {
  padding: 0 30px;
  text-align: center;
  margin-top: 10px;
  height: 360px
}

.video-study .read-learn .el-dialog .el-dialog__body p {
  text-align: left
}

.video-study .read-learn .el-dialog .el-dialog__body p span {
  display: block;
  color: #3d84ff;
  margin-top: 10px
}

.video-study .dialog-class .el-dialog {
  height: 430px
}

.video-study .dialog-class .el-dialog .el-dialog__body {
  text-align: left;
  padding: 0
}

.video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .el-scrollbar__wrap {
  padding: 0 30px
}

.video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-class .title, .video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-teacher .title {
  line-height: 24px;
  color: #2a2a2a;
  font-size: 14px;
  font-weight: 700;
  margin-bottom: 10px
}

.video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-class .title span, .video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-teacher .title span {
  height: 14px;
  width: 2px;
  background: #3d84ff;
  float: left;
  margin-right: 5px;
  margin-top: 5px
}

.video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-class .name, .video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-teacher .name {
  line-height: 24px;
  font-size: 14px;
  color: #2a2a2a;
  margin-bottom: 30px
}

.video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-class .teacher-info, .video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-teacher .teacher-info {
  margin-bottom: 21px
}

.video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-class .teacher-info span, .video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-teacher .teacher-info span {
  display: block
}

.video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-class .teacher-info .name, .video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-teacher .teacher-info .name {
  line-height: 24px;
  font-size: 14px;
  color: #2a2a2a;
  margin-bottom: 5px
}

.video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-class .teacher-info .num, .video-study .dialog-class .el-dialog .el-dialog__body .el-scrollbar .my-teacher .teacher-info .num {
  font-size: 12px;
  color: #777;
  line-height: 18px
}

.video-study .dialog .mask {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  opacity: .5;
  background: #000;
  z-index: 100
}

.video-study .dialog-read {
  width: 630px;
  height: 480px;
  top: 50%;
  left: 50%;
  position: fixed;
  transform: translate(-50%, -50%);
  background: #fff;
  z-index: 101
}

.video-study .dialog-read .el-dialog__header {
  border-bottom: 1px solid #ededed;
  padding: 20px 30px;
  padding-bottom: 15px;
  position: relative
}

.video-study .dialog-read .el-dialog__header h4 {
  font-size: 18px;
  color: #2a2a2a;
  line-height: 30px
}

.video-study .dialog-read .el-dialog__header p {
  font-size: 12px;
  color: #3d84ff;
  position: relative;
  line-height: 18px
}

.video-study .dialog-read .el-dialog__header .iconguanbi {
  position: absolute;
  top: 30px;
  right: 30px;
  font-size: 20px;
  color: #777;
  cursor: pointer
}

.video-study .dialog-read .el-dialog__body {
  padding: 0
}

.video-study .dialog-look-ans .el-dialog {
  position: relative
}

.video-study .dialog-look-ans .el-dialog .el-dialog__body {
  padding: 0 65px
}

.video-study .dialog-look-ans .el-dialog .el-dialog__footer {
  padding: 0;
  text-align: center;
  position: absolute;
  bottom: 20px;
  width: 100%
}

.video-study .dialog-look-ans .el-dialog .el-dialog__footer .btn {
  background: #3d84ff;
  width: 120px;
  height: 40px;
  text-align: center;
  color: #fff;
  border: 1px solid #3d84ff;
  border-radius: 0
}

.video-study .dialog-look-ans .el-dialog .el-dialog__footer .btn:hover {
  background: rgba(61, 132, 255, .8)
}

.video-study .dialog-look-ans .el-dialog .el-dialog__footer .cancel {
  background: #fff;
  border: 1px solid #ededed;
  color: #2a2a2a
}

.video-study .dialog-look-ans .el-dialog .el-dialog__footer .cancel:hover {
  background: #ededed
}

.video-study .dialog-look-habit .el-dialog {
  width: 500px;
  height: 346px;
  border-radius: 2px
}

.video-study .dialog-look-habit .el-dialog .el-dialog__header {
  padding: 20px 30px;
  padding-bottom: 15px;
  border-bottom: 1px solid #ededed
}

.video-study .dialog-look-habit .el-dialog .el-dialog__title {
  font-weight: 700
}

.video-study .dialog-look-habit .el-dialog .el-dialog__headerbtn {
  right: 30px
}

.video-study .dialog-look-habit .el-dialog .el-dialog__close {
  color: #777;
  font-size: 18px
}

.video-study .dialog-look-habit .el-dialog .el-dialog__body {
  padding: 0 40px;
  text-align: left;
  margin-top: 20px
}

.video-study .dialog-look-habit .el-dialog .el-dialog__body p {
  font-size: 14px;
  color: #2a2a2a;
  line-height: 24px
}

.video-study .dialog-look-habit .el-dialog .el-dialog__body p a {
  color: #3d84ff;
  cursor: pointer
}

.video-study .dialog-look-habit .el-dialog .el-dialog__footer {
  padding: 0;
  text-align: center;
  position: absolute;
  bottom: 30px;
  left: 50%;
  width: 500px;
  transform: translateX(-50%);
  -webkit-transform: translateX(-50%);
  -moz-transform: translateX(-50%);
  -ms-transform: translateX(-50%);
  -o-transform: translateX(-50%)
}

.video-study .dialog-look-habit .el-dialog .el-dialog__footer .btn {
  background: #3d84ff;
  width: 140px;
  height: 32px;
  line-height: 32px;
  text-align: center;
  color: #fff;
  border: 0;
  padding: 0;
  border-radius: 2px
}

.video-study .dialog-look-habit .el-dialog .el-dialog__footer .btn:hover {
  background: rgba(61, 132, 255, .8)
}

.video-study .dialog-look-habit .el-dialog .habit-teshu {
  margin-top: 10px;
  text-align: left;
  font-size: 12px;
  color: #f94f17;
  line-height: 18px;
  padding: 10px;
  background: #fef5e2
}

.video-study .dialog-learn-habit .el-dialog {
  width: 570px;
  height: 520px;
  border-radius: 2px
}

.video-study .dialog-learn-habit .el-dialog .el-dialog__header {
  padding: 20px 30px;
  padding-bottom: 15px
}

.video-study .dialog-learn-habit .el-dialog .el-dialog__title {
  font-weight: 700
}

.video-study .dialog-learn-habit .el-dialog .el-dialog__headerbtn {
  right: 30px
}

.video-study .dialog-learn-habit .el-dialog .el-dialog__close {
  color: #777;
  font-size: 18px
}

.video-study .dialog-learn-habit .el-dialog .el-dialog__body {
  padding: 0;
  text-align: left
}

.video-study .preschool-Mustread-div {
  padding: 0 30px 55px;
  background: #fff
}

.video-study .preschool-Mustread-div .studyExam-div {
  border-top: 1px solid #ededed;
  border-bottom: 1px solid #ededed;
  padding: 15px 0;
  text-align: center
}

.video-study .preschool-Mustread-div .studyExam-div .studytime-div {
  margin-bottom: 15px
}

.video-study .preschool-Mustread-div .studyExam-div .studytime-div .studytime-p1 {
  color: #333;
  line-height: 26px;
  font-weight: 700;
  font-size: 16px
}

.video-study .preschool-Mustread-div .studyExam-div .studytime-div .studytime-p2 {
  font-size: 12px;
  color: #2a2a2a;
  line-height: 18px;
  margin-top: 5px
}

.video-study .preschool-Mustread-div .studyExam-div .Examtime-div .Examtime-p1 {
  color: #333;
  line-height: 26px;
  font-weight: 700;
  font-size: 16px
}

.video-study .preschool-Mustread-div .studyExam-div .Examtime-div .Examtime-p2 {
  font-size: 12px;
  color: #2a2a2a;
  line-height: 18px;
  margin-top: 5px
}

.video-study .preschool-Mustread-div .studyhint-p {
  font-size: 12px;
  color: #666;
  line-height: 18px;
  margin-top: 10px;
  text-align: center
}

.video-study .AchievementRules-div {
  margin-top: 40px
}

.video-study .AchievementRules-div h1 {
  font-size: 18px;
  color: #000;
  line-height: 30px;
  font-weight: 700
}

.video-study .AchievementRules-div h2 {
  font-size: 14px;
  color: #2a2a2a;
  letter-spacing: .07px;
  line-height: 24px;
  font-weight: 700;
  margin-top: 18px
}

.video-study .AchievementRules-div .p1 {
  font-size: 14px;
  color: #777;
  letter-spacing: .07px;
  line-height: 24px
}

.video-study .AchievementRulesbg-div {
  background: #f7f9fe;
  border-radius: 2px;
  padding: 20px 25px
}

.video-study .AchievementRulesbg-div ul li {
  font-size: 14px;
  color: #777;
  letter-spacing: .07px;
  line-height: 24px
}

.video-study .AchievementRulesbg-div ul .bulefont {
  color: #3d84ff
}

.video-study .AchievementRuleslist {
  margin-bottom: 45px
}

.video-study .nano-content-all {
  height: 370px
}

.video-study .el-pagination {
  margin-bottom: 18px
}

.video-study .el-pagination .el-pager li {
  background: #fff;
  border: 1px solid #ededed;
  border-radius: 12px;
  font-size: 12px;
  color: #2a2a2a
}

.video-study .el-pagination .el-pager .active, .video-study .el-pagination .el-pager li:hover {
  background: #3d84ff;
  color: #fff;
  border: 1px solid #3d84ff
}

.video-study-black .box-content .box-left .left-top {
  background: #1d1d1d;
  box-shadow: inset -1px 0 0 0 #2a2a2a;
  color: #777
}

.video-study-black .box-content .box-left .left-top .videotop_lesson, .video-study-black .box-content .box-left .left-top .videotop_lesson_tit {
  color: #bfbfbf
}

.video-study-black .box-content .box-left .left-top .videotop_all ul li em, .video-study-black .box-content .box-left .left-top .videotop_all ul li span {
  color: #777
}

.video-study-black .box-content .box-left .left-top .videotop_all ul li:hover em, .video-study-black .box-content .box-left .left-top .videotop_all ul li:hover span {
  color: #bfbfbf
}

.video-study-black .box-content .box-right {
  background: #1d1d1d
}

.video-study-black .box-content .box-right .newListTest li {
  color: #777
}

.video-study-black .box-content .box-right .newListTest li:hover {
  background: #2a2a2a
}

.video-study-black .box-content .box-right .newListTest li a {
  color: #777
}

.video-study-black .box-content .box-right .newListTest li a em {
  color: #bfbfbf
}

.video-study-black .box-content .box-right .newListTest li a div {
  margin-top: 5px
}

.video-study-black .box-content .box-right .topicTitle {
  background: #2a2a2a;
  box-shadow: inset 0 -1px 0 0 #2a2a2a
}

.video-study-black .box-content .box-right .topicTitle ul .tabTitle {
  color: #bfbfbf
}

.video-study-black .box-content .box-right .list {
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/2e21819f5b664b67b29113d2ba582974.png) 68px 0 repeat-y
}

.video-study-black .box-content .box-right .list li:hover {
  background: #2a2a2a;
  color: #ededed
}

.video-study-black .box-content .box-right .list li:hover .chapter-em {
  background: url(https://image.zhihuishu.com/zhs_yufa_150820/ablecommons/demo/201910/2592813a3dee4adb9687bd4e4805c8ba.png) no-repeat
}

.video-study-black .box-content .box-right .list li .catalogue_title3 {
  color: #777
}

.video-study-black .box-content .box-right .list li .catalogue_title4 {
  color: #999
}

.video-study-black .box-content .box-right .list li .catalogue_title {
  color: #ededed
}

.video-study-black .box-content .box-right .list li .time {
  color: #777
}

.video-study-black .box-content .box-right .list li .Sectionmark-em {
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/bcefe48e05f44b38ab1bf8615c6ca3d0.png) no-repeat
}

.video-study-black .box-content .box-right .list .chapter-test .name {
  color: #ededed
}

.video-study-black .box-content .box-right .list .chapter-test .iconfont {
  color: #777
}

.video-study-black .box-content .box-right .list .chapter-test .iconyiwancheng {
  color: #3d84ff
}

.video-study-black .box-content .box-right .list .font_gray_inclined .chapter-em {
  background: url(https://image.zhihuishu.com/zhs_yufa_150820/ablecommons/demo/201910/92769ecc02ba46b39d7ae8785def5396.png) no-repeat
}

.video-study-black .box-content .box-right .list .current_play {
  background: rgba(61, 132, 255, .15);
  color: #3d84ff
}

.el-message-box {
  border-radius: 2px
}

.el-message-box .el-message-box__header {
  padding: 15px 30px
}

.el-message-box .el-message-box__header span {
  font-weight: 700
}

.el-message-box .el-message-box__header .el-message-box__headerbtn {
  right: 30px
}

.el-message-box .el-message-box__header .el-message-box__close {
  color: #777;
  font-size: 18px
}

.el-message-box .el-message-box__header .el-message-box__close:before {
  background: inherit !important;
  color: #777 !important
}

.el-message-box .el-message-box__content {
  padding: 0;
  text-align: center
}

.el-message-box .el-message-box__content .el-message-box__message {
  padding: 0
}

.el-message-box .el-message-box__content .el-message-box__message p {
  text-align: center;
  color: #2a2a2a;
  line-height: 24px
}

.el-message-box .el-message-box__content .img {
  background: url(//image.zhihuishu.com/zhs/ablecommons/demo/201907/4f4b9902b4ca4cd18a66978a86bc181b.png) no-repeat;
  background-size: 100% 100%;
  display: block;
  margin-bottom: 5px;
  height: 60px;
  width: 60px;
  position: inherit;
  transform: inherit;
  display: inline-block
}

.el-message--info {
  height: 50px;
  line-height: 50px;
  color: #fff;
  background: #7e7e7c;
  font-size: 12px;
  border-radius: 50px;
  padding: 0 20px;
  top: 50% !important;
  left: 50%;
  transform: translate(-50%, -50%);
  -webkit-transform: translate(-50%, -50%);
  -moz-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  -o-transform: translate(-50%, -50%)
}

.el-message--info .el-icon-info {
  display: none
}

@keyframes showSmallSty {
  0% {
    width: 42px
  }
  to {
    width: 300px
  }
}

@-webkit-keyframes showSmallSty {
  0% {
    width: 42px
  }
  to {
    width: 300px
  }
}

@keyframes showBigSty {
  0% {
    width: 300px
  }
  to {
    width: 42px
  }
}

@-webkit-keyframes showBigSty {
  0% {
    width: 300px
  }
  to {
    width: 42px
  }
}

.swiper {
  position: relative;
  height: 100%;
  width: 100%;
  z-index: 1000000
}

.swiper .close {
  position: fixed;
  top: 20px;
  right: 20px;
  z-index: 20;
  cursor: pointer
}

.swiper .close i {
  font-size: 24px;
  color: #fff
}

.swiper .swiper-mask {
  background: rgba(16, 17, 28, .7);
  z-index: 5
}

.swiper .el-carousel, .swiper .swiper-mask {
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%
}

.swiper .el-carousel {
  z-index: 10
}

.swiper .el-carousel .el-carousel__container {
  height: 100%;
  overflow: hidden
}

.swiper .el-carousel .el-carousel__arrow {
  background-color: rgba(165, 167, 192, .5);
  width: 48px;
  height: 48px
}

.swiper .el-carousel [class*=" el-icon-"], .swiper .el-carousel [class^=el-icon-] {
  color: #3d4059;
  font-size: 20px;
  font-weight: 600
}

.swiper .el-carousel .el-carousel__indicators {
  display: none
}

.swiper .el-carousel .el-carousel__item {
  text-align: center;
  margin-top: calc(50vh - 230px)
}

.swiper .el-carousel .swiper-img {
  max-width: 690px;
  height: 460px;
  -o-object-fit: cover;
  object-fit: cover
}

.swiper .swiper-num {
  position: absolute;
  top: 50%;
  left: 50%;
  font-size: 24px;
  color: #a5a7c0;
  font-family: priceFont;
  margin-top: 240px
}

.swiper .swiper-num span {
  font-size: 32px;
  color: #fff
}
</style>
