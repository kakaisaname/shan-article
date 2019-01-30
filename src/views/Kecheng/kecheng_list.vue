<template>
  <div class="match-list">
    <cube-scroll
      ref="scroll"
      :data="kechengs" 
      :options="options"
      @pulling-down="onPullingDown"
      @pulling-up="onPullingUp">
      <ul class="match-inner">
          <li v-for="(item, index) in kechengs" :key="index" class="match-item" @click="lookDeta(item.id)">
            <!-- <a href="http://www.baidu.com">   -->
              <img :src="item.smallimg_url" alt="" class="item-img" >
              <div class="item-info">
                  <div class="item-float">
                      <p class="item-title">{{ item.title }}</p>
                      <p class="item-desc">{{ item.desc }}</p>
                  </div>
                  <!-- <cube-button :light="true" :inline="true" class="item-button">查看详情</cube-button> -->
              </div>
            <!-- </a> -->
          </li>
      </ul>
    </cube-scroll>
  </div>
</template>

<script>
import axios from 'axios'
import { Message } from 'element-ui'
const UP = 'up'
const DOWN = 'down'
// 处理数据


export default {
  name: 'KechengList',
  props: {
        kechengs: Array
  },
  data () {
    return {
      options: {
        scrollbar: {
          fade: true
        },
        pullDownRefresh: {
          threshold: 90,
          stop: 50,
          txt: '刷新成功'
        },
        pullUpLoad: {
          threshold: 0,
          txt: {
            more: '加载更多',
            noMore: '没有更多的文章啦'
          }
        },
        click: false
      }
    }
  },
  methods: {
    subscribe () {
      this.subscribeDialog.show()
    },
    onPullingDown () {
      this.loadMatch('down')
    },
    onPullingUp () {
      this.loadMatch('up')
    },
    loadMatch (type) {
      setTimeout(() => {
        if (Math.random() > 0.5) {
          let match = []
          for (let index = 5; index > 0; index--) {
            // match.push(this.recipeList[index])
          }
          if (type === DOWN) {
            this.kechengs.unshift(...match)
          } else if (type === UP) {
            this.kechengs = this.kechengs.concat(match)
          }
        } else {
          this.$refs.scroll.forceUpdate()
          if (type === UP) {
            setTimeout(() => {
              this.$refs.scroll.scroll.scrollBy(0, 64, 800)
            }, 1000)
          }
        }
      }, 1000)
    },
    lookDeta (id) {
      console.log(1)
        window.location.href = "http://www.baidu.com"
    },
    mounted () {
      console.log(1)
    }
  }
}
</script>

<style lang="stylus">
@import '~@/common/stylus/mixin.styl';
.match-list
  height: 600px
  background-color: #E2E5EA
  .match-inner
    background-color: #FFFFFF
    .match-item
    //   height:30px;  
      border-bottom: 1px solid #E4E4E4
      padding: 10px 0
      // display: flex
      justify-content: space-around
      .item-img       //图片的宽和高
        display: inline-block
        height: 50px
        margin-bottom: 7px
        width:50px
        padding 1%
      .item-info
        flex 1  //1自动撑开
        // height 100%
        padding .1rem
        min-width 0  //min-width 属性为给定元素设置最小宽度。它可以阻止 width 属性的应用值小于 min-width 的值。
        .item-float
          float left
          text-align left //加这个，不加这个的话两行字不对齐
          .item-title
              line-height 20px
              font-size 12px;
              ellipsis()
          .item-desc
              line-height 15px
              font-size 10px
              color #ccc
              ellipsis()
        // .item-button
            // float left
            // line-height 10px
            // margin-top 2px
            // background #ff9300
            // padding 0 2px      //上下0  左右.1rem
            // border-radius 3px  //3像素  相当于0.06
            // color   #fff
</style>
