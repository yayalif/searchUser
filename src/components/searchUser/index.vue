<template>
    <div class="search-user" ref="searchUser">
    <div class="finished-user-list">
      <div class="item" v-for="(item, index) in finishedLists" :key="index" >
        <span class="value"> {{ item }} </span>
        <div class="delete-icon">
        </div>
      </div>
    </div>
    <div class="input-user">
      <input type="text" v-model="input" @input="searchUser" ref="input">
      <div class="select-user-list" v-show="selectLists.length > 0">
        <div class="item" v-for="(item, index) in selectLists" :key="index" @click="chooseUser(item)">
          {{ item }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'searchUser',
  data () {
    return {
      input: '',
      // 下拉用户列表
      selectLists: [
      ],
      // 已选中的
      finishedLists: []

    }
  },
  methods: {
    searchUser () {
      this.selectLists = ['', '@cmrh.com', '@cmft.com'].map((item) => {
        return this.input + item
      })
    },
    chooseUser (value) {
      this.input = value
      this.input = ''
      this.finishedLists.push(value)
      this.selectLists = []
      // this.$refs.input.scrollLeft = this.$refs.input.scrollWidth
      // this.$refs.searchUser.scrollLeft = this.$refs.searchUser.scrollWidth - this.$refs.searchUser.clientWidth/2*3
      console.log(this.$refs.searchUser.clientWidth/2, 'this.$refs.input.scrollWidth')
      console.log(this.$refs.searchUser.scrollWidth, 'this.$refs.searchUser.scrollWidth')
      console.log(this.$refs.searchUser.scrollLeft, 'this.$refs.searchUser.scrollLeft')

    },
    deleteUser(item, index) {
      this.finishedLists.splice(index, 1)
    }
  }


}
</script>

<style lang="scss" scoped>
.search-user-container {
  width: 100%;
  // height: 100%;
}
  .search-user {
    margin-top: 5rem;
    width: 7rem;
    height: .7rem;
    overflow-x: auto;
    display:flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    border: 1px solid rgb(160, 197, 221);
    z-index: 10;
    .input-user {
      min-width:50%;
      height: .5rem;
          flex: 1;
          // border: 1px solid #666;
        .select-user-list {
          position: absolute;
          display: flex;
          flex-direction: column;
          align-items: center;
          justify-content: center;
          border: 1px solid #666;
          .item {
            width: 100%;
            box-sizing: border-box;
            padding: .12rem;
            font-size: .32rem;
            border-bottom: 1px solid rgb(51,51,51);
            &:last-child {
              border-bottom: none;
            }
        }
      }
    }
    .finished-user-list {
      display: flex;
      flex-direction: row;
      justify-content: center;
      max-width: 50%;
      height: .5rem;
      overflow-x: scroll;
      padding: .1rem;
      .item {
        flex: 1;
        height: .5rem;
        border: 1px solid greenyellow;
        white-space: nowrap;
        border-radius: 4px;
        .value {
          max-width: 50%;
          vertical-align:top;
          line-height: .5rem;
          padding: .02rem;
          font-size: .32rem;
          margin-right: .02rem;
          overflow: hidden;
          text-overflow: ellipsis;
          white-space: nowrap;/*规定段落中的文本不进行换行 */
        }
        .delete-icon {
          vertical-align:top;
          display: inline-block;
          padding-top: .05rem;
          width: .3rem;
          height: .3rem;
          border-radius: 50%;
          border: 1px solid rgb(103,103,103);
        }
      }
    }
  }
  input {
    width: 100%;
    height: 100%;
    background:none;  
    outline:none;  
    border:none;
    vertical-align: top;
    font-size: .42rem;
    line-height: .42rem;
    border-radius: 4px;
  }
</style>
<style>
* {
  padding: 0;
  margin: 0;
}

</style>