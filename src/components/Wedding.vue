<template>
  <div>
    <div class="wedding-user-info">
      <div class="wedding-user-info-left">
        <img
          src="https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=347837335,1617350328&fm=27&gp=0.jpg"
        >
      </div>
      <div class="wedding-user-info-right">
        <div class="wedding-user-info-name">单尾羊羊</div>
        <div class="wedding-user-info-sub">
          <img src="../assets/location.png">
          <label>北京</label>
        </div>
        <div class="wedding-user-info-sub">
          <img src="../assets/history.png">
          <label>婚期：2019-7-7</label>
        </div>
      </div>
    </div>
    <div class="wedding-cell">
      <div class="wedding-common-cell-header">
        <div class="wedding-common-cell-header-title">婚礼风格愿景板</div>
      </div>
      <div class="wedding-content">
        <div class="wedding-photo-board">
          <vue-gallery-pictures
            :items="items"
            :boxInitRatio=77
            :box-container-class="boxContainerClass"
            last-line-mode="origin"
            @loaded="loaded"
            @error="error"
          >
            <template slot-scope="scope">
              <span v-show="scope.item.error">error</span>
              <span v-show="scope.item.loading && !scope.item.error">loading</span>
            </template>
          </vue-gallery-pictures>
        </div>
      </div>
    </div>
    <div class="wedding-cell wedding-photo-board">
      <div class="wedding-common-cell-header">
        <div class="wedding-common-cell-header-title">婚礼性格</div>
      </div>
      <div class="wedding-cell-content">
        <p>
          我理想的婚礼风格是浪漫多彩、优雅、又富有时尚感的设计，理想的宴会场西餐会所、野奢酒店或城市酒店。
        </p>
      </div>
    </div>
    <div class="wedding-cell wedding-photo-board">
      <div class="wedding-common-cell-header">
        <div class="wedding-common-cell-header-title">色彩风格</div>
      </div>
      <div class="wedding-photo-board-content">
        <div></div>
      </div>
    </div>
    <div class="wedding-cell van-hairline--bottom wedding-photo-board">
      <div class="wedding-common-cell-header">
        <div class="wedding-common-cell-header-title">必要记录</div>
      </div>
      <div class="wedding-photo-board-content"></div>
    </div>
    <div>
      <button>重新测试</button>
    </div>
  </div>
</template>

<script>
import VueGalleryPictures from "vue-gallery-pictures";
import axios from "axios";

export default {
  components: {
    VueGalleryPictures
  },
  data() {
    return {
      items: [],
      boxContainerClass: "container-class"
    };
  },
  methods: {
    loaded(item) {
      // console.log(item.loading);
    },
    error(item, e) {
      // console.log(item.error, e);
    }
  },
  created() {
    const basePath = "https://xieranmaya.github.io/images/cats";
    axios.get(`${basePath}/cats.json`).then(res => {
      res.data.forEach(item => {
        item.src = basePath + "/" + item.url;
        item.loading = true;
        item.error = false;
        item.width = parseInt(item.width / 30);
        item.height = parseInt(item.height / 30);
      });
      console.log(res.data);
      this.items = res.data.slice(0, 5);
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
  }
  &-user-info-sub {
    display: flex;
    flex-direction: row;
    margin-left: 13px;
    margin-top: 8px;
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
    max-height: 200px;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    overflow-y: hidden;
  }
  &-photo-board {
    margin: 10px 10px 0px;
    padding-bottom: 20px;
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
</style>