<template>
  <div class="topicdetail">
    <div class="content">
      <div class="detail" v-if="goods_desc">
        <wxParse :content="goods_desc" />
      </div>
    </div>
    <div class="list">
      <p class="title">专题推荐</p>
      <div class="item" v-for="(item,index) in recommendList" :key="index">
        <img :src="item.scene_pic_url" alt="">
        <p>{{item.title}}</p>
      </div>
    </div>
  </div>
</template>

<script>
import wxParse from 'mpvue-wxparse'
import {get} from '../../utils'
export default {
  components: {
    wxParse
  },
  data () {
    return {
      goods_desc: '',
      id: '',
      recommendList: []
    }
  },
  mounted() {
    this.id = this.$root.$mp.query.id
    this.getListData()
  },
  methods: {
    async getListData () {
      const data = await get('/topic/detailaction',{
        'id': this.id
      })
      console.log(data)
      this.goods_desc = data.data.content
      this.recommendList = data.recommendList
      
    }
  }
}
</script>

<style  lang="less" scoped>
.topicdetail {
  .list {
    width: 690rpx;
    height: auto;
    margin: 0 30rpx;
    .title {
      text-align: center;
      background: #f4f4f4;
      font-size: 30rpx;
      color: #999;
      padding: 30rpx 0;
    }
    .item {
      width: 100%;
      padding: 24rpx 24rpx 30rpx 24rpx;
      margin-bottom: 30rpx;
      background: #fff;
      box-sizing: border-box;
      img {
        height: 278rpx;
        width: 642rpx;
        display: block;
      }
      p {
        display: block;
        margin-top: 30rpx;
        font-size: 28rpx;
      }
    }
  }
}
</style>