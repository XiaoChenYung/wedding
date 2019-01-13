<template>
  <div>
    <div class="wedding-user-info">
      <div class="wedding-user-info-left">
        <img :src="userInfo.avatar">
      </div>
      <div class="wedding-user-info-right">
        <div class="wedding-user-info-name">{{userInfo.nickname}}</div>
        <!-- <div class="wedding-user-info-sub">
          <img src="../assets/location.png">
          <label>未知</label>
        </div>-->
        <div class="wedding-user-info-sub">
          <img src="../assets/history.png">
          <label>婚期：{{userInfo.weddingDate}}</label>
        </div>
      </div>
    </div>
    <div class="wedding-cell">
      <div class="wedding-common-cell-header">
        <div class="wedding-common-cell-header-title">婚礼风格愿景板</div>
      </div>
      <div class="wedding-content">
        <div class="wedding-photo-board">
          <div>
            <span :style="item.stype" v-for="(item, index) in wedding.marrayImages" :key="index">
              <img class="photo-image" v-if="index % 2 == 0" :src="item.url" alt="">
            </span>
          </div>
          <div>
            <span :style="item.stype" v-for="(item, index) in wedding.marrayImages" :key="index">
              <img class="photo-image" v-if="index % 2 == 1" :src="item.url" alt="">
            </span>
          </div>
        </div>
      </div>
    </div>
    <div class="wedding-cell">
      <div class="wedding-common-cell-header">
        <div class="wedding-common-cell-header-title">婚礼性格</div>
      </div>
      <div class="wedding-cell-content">
        <p>
          我理想的婚礼风格是
          <span v-for="(item, index) in wedding.textTags" :key="index">
            <span class="tags">{{item}}</span>
            <span v-if="index < wedding.textTags.length - 1">、</span>
          </span>
        </p>
        <p>
          理想的宴会场地是
          <span v-for="(item, index) in wedding.placeTags" :key="index">
            <span class="tags">{{item}}</span>
            <span v-if="index < wedding.placeTags.length - 1">、</span>
          </span>
        </p>
      </div>
    </div>
    <div class="wedding-cell">
      <div class="wedding-common-cell-header">
        <div class="wedding-common-cell-header-title">色彩风格</div>
      </div>
      <div class="wedding-cell-content">
        <div class="color-tip">{{wedding.swatchName}}</div>
        <div class="circle-content">
          <div v-for="(item, index)  in wedding.colors" :key="index" :style="item" class="circle"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import VueGalleryPictures from "vue-gallery-pictures";
import { Toast } from "vant";
import axios from "axios";

export default {
  components: {},
  data() {
    return {
      wedding: {},
      userInfo: {},
      boxContainerClass: "container-class"
    };
  },
  methods: {
    // loaded(item) {
    //   // console.log(item.loading);
    // },
    // error(item, e) {
    //   // console.log(item.error, e);
    // }
  },
  created() {
    Toast.loading({
      mask: false,
      message: "加载中..."
    });
    let token = this.$route.query.token
    console.log(token)
    const weddingPath =
      "http://120.27.11.247/api/index/marryStyle?token=" + token;
    const userInfoPath =
      "http://120.27.11.247/api/user/getInfo?token=" + token;
    axios
      .get(userInfoPath)
      .then(res => {
        let item = res.data.data;
        item.weddingDate = item.marry_time_str.substring(0, 9);
        this.userInfo = item;
        return axios.get(weddingPath);
      })
      .then(res => {
        Toast.clear();
        let item = res.data.data;
        item.colors = item.colors.map(color => {
          color = "background-color: " + color;
          return color;
        });
        this.wedding = res.data.data;
      })
      .catch(err => {
        Toast.fail(err.message);
      });
  }
};
</script>

<style lang="less">
.wedding {
  &-user-info {
    padding: 29px 40px;
    display: flex;
    flex-direction: row;
    margin-bottom: 8px;
    background: #ffffff;
    box-shadow: 0 3px 10px 0 rgba(0, 0, 0, 0.09);
  }
  &-user-info-left img {
    width: 74px;
    height: 74px;
    border-radius: 37px;
    margin-top: 6px;
  }
  &-user-info-name {
    font-family: PingFangSC-Medium;
    font-size: 16px;
    color: #000000;
    letter-spacing: 0;
    text-align: center;
    line-height: 30px;
    text-align: left;
    margin-left: 13px;
    margin-top: 10px;
  }
  &-user-info-sub {
    display: flex;
    flex-direction: row;
    margin-left: 13px;
    margin-top: 10px;
  }
  &-user-info-sub img {
    width: 18px;
    height: 18px;
    margin-top: 1px;
  }
  &-user-info-sub label {
    font-family: PingFangSC-Regular;
    font-size: 14px;
    color: #555555;
    letter-spacing: 0;
    line-height: 20px;
    margin-left: 3px;
  }
  &-cell {
    background: #ffffff;
    box-shadow: 0 3px 10px 0 rgba(0, 0, 0, 0.09);
    border-radius: 13px;
    margin: 0 10px 8px;
  }
  &-common-cell-header {
    height: 51px;
    display: flex;
    flex-direction: row;
    border-bottom: 1px solid #eeeeee;
  }
  &-common-cell-header-title {
    font-family: PingFangSC-Medium;
    font-size: 16px;
    color: #000000;
    letter-spacing: 0;
    line-height: 51px;
    margin-left: 18px;
  }
  &-cell-content {
    // height: 50px;
    // max-height: 200px;
    // display: flex;
    // flex-direction: row;
    // flex-wrap: nowrap;
    // overflow-y: hidden;
    padding-bottom: 10px;
  }
  &-photo-board {
    height: 240px;
    overflow-x: scroll;
    overflow-y: hidden;
    white-space: nowrap;
  }
}
.container-class {
  margin: 4px;
  border-radius: 5px;
}
.gallery-layout {
  flex-direction: row;
}
.gallery-pic-box-img {
  border-radius: 5px;
}
.gallery-layout {
  overflow: hidden;
}
p {
  padding: 0 13px;
  text-align: left;
}
.tags {
  color: #fd8124;
}
.circle-content {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
.circle {
  width: 54px;
  height: 54px;
  border-radius: 27px;
}
.color-tip {
  font-family: PingFangSC-Medium;
  font-size: 24px;
  color: #000000;
  letter-spacing: 0;
  line-height: 74px;
}
.photo-image {
  height: 100px;
  border-radius: 5px;
  margin-left: 10px;
  margin-top: 10px;
}
</style>