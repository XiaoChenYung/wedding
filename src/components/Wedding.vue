<template>
  <div>
    <div class="wedding-user-info">
      <div class="wedding-user-info-left">
        <img src alt>
      </div>
      <div class="wedding-user-info-right">
        <div class="wedding-user-info-name">单尾羊羊</div>
        <div class="wedding-user-info-sub">
          <img src="../assets/location.png">
          <label>北京</label>
        </div>
        <div class="wedding-user-info sub">
          <img src="../assets/history.png">
          <label>婚期：2019-7-7</label>
        </div>
      </div>
    </div>
    <div class="wedding-cell van-hairline--bottom wedding-photo-board">
      <div class="wedding-common-cell-header">
        <div class="wedding-common-cell-header-title">婚礼风格愿景板</div>
      </div>
      <div class="wedding-photo-board-content"></div>
    </div>
    <div class="wedding-cell wedding-photo-board">
      <div class="wedding-common-cell-header">
        <div>婚礼性格</div>
      </div>
      <div class="wedding-photo-board-content"></div>
    </div>
    <div class="wedding-cell wedding-photo-board">
      <div class="wedding-common-cell-header">
        <div>色彩风格</div>
      </div>
      <div class="wedding-photo-board-content"></div>
    </div>
    <div class="wedding-cell van-hairline--bottom wedding-photo-board">
      <div class="wedding-common-cell-header">
        <div>必要记录</div>
      </div>
      <div class="wedding-photo-board-content"></div>
    </div>
    <div>
      <button>重新测试</button>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="less">
.wedding {
  &-user-info {
    padding: 29px 40px;
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
  }
  &-common-cell-header-title {
    font-family: PingFangSC-Medium;
    font-size: 16px;
    color: #000000;
    letter-spacing: 0;
    line-height: 51px;
  }
  &-photo-board-content {
    height: 50px;
  }
}
</style>