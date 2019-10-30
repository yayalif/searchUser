<template>
  <div class="container">
    <div class="header">
        电影闲情
    </div>
    <div class="body" @touchstart="touchStart($event)" @touchmove="touchMove($event)" @touchend="touchEnd($event)" :style="{transform: 'translate3d(0,' + top + 'px, 0)'}">
       <header class="pull-refresh">
        <slot name="pull-refresh">
          <div class="down-tip" v-if="dropDownState==1">
            <!-- <img v-if="dropDownInfo.downImg" class="down-img" :src="require('../../assets/images/refreshAndReload/'+dropDownInfo.downImg)"> -->
            
            <span class="down-text">{{dropDownInfo.downText}}</span>
          </div>
          <div class="up-tip" v-if="dropDownState==2">
            <!-- <img v-if="dropDownInfo.upImg" class="up-img" :src="require('../../assets/images/refreshAndReload/'+dropDownInfo.upImg)"> -->
            <span class="up-text">{{dropDownInfo.upText}}</span>
          </div>
          <div class="refresh-tip" v-if="dropDownState==3">
            <!-- <img v-if="dropDownInfo.refreshImg" class="refresh-img" :src="require('../../assets/images/loading/'+dropDownInfo.refreshImg)"> -->
            <span class="refresh-text">{{dropDownInfo.refreshText}}</span>
          </div>
        </slot>
      </header>
      <div class="time">
        最新更新时间 2019-03-26 12：00：00
      </div>
      <div class="items">
        <div class="item" v-for="(item, index) in dataList" :key="index">
          <img src="./img/1.jpg" >
          <div class="info">
            <div class="name">
              美女与野兽 {{ item }}
            </div>
            <div class="time">
              上映时间：2019-08-12
            </div>
            <div class="place">
              大地电影院
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="footer">
      电影闲情
    </div>

  </div>
</template>

<script>
export default {
  data () {
    return {
      dataList: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12],
      defaultOffset: 50, // 默认高度, 相应的修改.releshMoudle的margin-top和.down-tip, .up-tip, .refresh-tip的height
      top: 0,
      scrollIsToTop: 0,
      startY: 0,
      isDropDown: false, // 是否下拉
      isRefreshing: false, // 是否正在刷新
      dropDownState: 1, // 显示1:下拉可以刷新, 2:松开立即刷新, 3:正在刷新数据中...
      dropDownInfo: {
        downText: '下拉可以刷新',
        downImg: 'arrow.png',
        upText: '松开立即刷新',
        upImg: 'arrow.png',
        refreshText: '正在刷新数据...',
        refreshImg: 'loading.png'
      }
    }
  },
  mounted () {

  },
  methods: {
    touchStart (e) {
      this.startY = e.targetTouches[0].pageY
    },
    touchMove (e) {
      this.scrollIsToTop = document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop // safari 获取scrollTop用window.pageYOffset
      if (e.targetTouches[0].pageY > this.startY) {
        console.log(this.scrollIsToTop, 'this.scrollIsToTop')
        // 下拉
        this.isDropDown = true
        if (this.scrollIsToTop === 0 && !this.isRefreshing) {
          // 拉动的距离
          let diff = e.targetTouches[0].pageY - this.startY - this.scrollIsToTop
          this.top = Math.pow(diff, 0.8) + (this.dropDownState === 3 ? this.defaultOffset : 0)
          console.log(this.top, this.dropDownState === 3, 'this.top')
          if (this.top >= this.defaultOffset) {
            this.dropDownState = 2
            console.log('松开立即刷新')
            e.preventDefault()
          } else {
            console.log('下拉可以刷新')
            this.dropDownState = 1
            // 去掉会导致ios无法刷新
            e.preventDefault()
          }
        }
      } else {
        this.isDropDown = false
        this.dropDownState = 1
      }
    },
    touchEnd () {
      if (this.isDropDown && !this.isRefreshing) {
        if (this.top >= this.defaultOffset) {
          // do refresh
          this.refresh()
          this.isRefreshing = true
        } else {
          // cancel refresh
          this.isRefreshing = false
          this.isDropDown = false
          this.dropDownState = 1
          this.top = 0
        }
      }
    },
    /**
     * 刷新
     */
    refresh () {
      this.dropDownState = 3
      this.top = this.defaultOffset
      console.log(this.top, 'refresh')
      // 这是全是静态数据,延时1200毫秒，给用户一个刷新的感觉，如果是接口数据的话，直接调接口即可
      setTimeout(() => {
        // this.onRefresh(this.refreshDone)
        this.onRefresh()
        this.refreshDone()
      }, 2000)
    },
      /**
     * 刷新完成
     */
    refreshDone () {
      this.isRefreshing = false
      this.isDropDown = false
      this.dropDownState = 1
      this.top = 0
    },
    /**
     * 刷新数据
     */
    onRefresh () {
      for(let i =0 ; i < 5; i++) {
        this.dataList.unshift(Math.ceil(Math.random()*100))
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  .container {
    width: 100%;
    height:100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    .header {
      width: 100%;
      height:40px;
      background:chocolate;
      text-align:center;
      font-size: 24px;
      position: fixed;
      top: 0;
      z-index: 10;
    }
    .pull-refresh {
      width: 100%;
      color: #999;
      transition-duration: 200ms;
      font-size: 24px;
      height: 32px;
    }
    .body {
      flex: 1;
      width: 100%;
      position: relative;
      top: 8px;
      -webkit-overflow-scrolling: touch; /* ios5+ */
      .time {
        background:#999;
        width: 100%;
        height: 36px;
        text-align: center;
        line-height: 36px;
      }
      .items {
        flex: 1;
        width: 100%;
        .item {
          display: flex;
          flex-direction: row;
          img {
            width: 140px;
            flex-shrink: 0;
          }
          border-bottom: 1px solid #999; 
        }
      }
    }
    .footer {
      width: 100%;
      height:40px;
      background:darksalmon;
      text-align:center;
      font-size: 24px;
    }
  }
</style>