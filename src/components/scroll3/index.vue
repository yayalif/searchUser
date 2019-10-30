<template>
  <div class="container">
    <div class="header">
        电影闲情
    </div>
    <v-refresh :on-refresh="onRefresh">
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
    </v-refresh>
    <div class="footer">
      电影闲情
    </div>

  </div>
</template>

<script>
import downLoad from "./downLoad";
export default {
  components: {
    'v-refresh' : downLoad
  },
  data () {
    return {
      dataList: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12],
    }
  },
  mounted () {

  },
  methods: {
    /**
     * 刷新数据
     */
    onRefresh (done) {
      new Promise((resolve, reject) => {
        setTimeout(() => {
          for(let i =0 ; i < 5; i++) {
            this.dataList.unshift(Math.ceil(Math.random()*100))
          }
          done()
          resolve()
        }, 100);
      })
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
    }
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
    .footer {
      width: 100%;
      height:40px;
      background:darksalmon;
      text-align:center;
      font-size: 24px;
    }
  }
</style>