<template>
  <div class="recommend">
    <div>
      <div v-if="recommends.length" class="slider-wrapper">
        <slider>
          <div v-for="item in recommends"  ref="sliderWrapper">
            <a :href="item.linkUrl">
              <img :src="item.picUrl" alt="">
            </a>
          </div>
        </slider>
      </div>
      <div class="recommend-list">
        <h1 class="list-title">热门歌单推荐</h1>
      </div>
    </div>
  </div>
</template>

<script>
import {getRecommend, getDiscList} from '../../api/getrecommend'
import {ERR_OK} from '../../api/config'
import Slider from '../../base/slider/slider'
export default {
  data () {
    return {
      recommends: []
    }
  },
  created () {
    this._getrecommend()
    this._getDiscList()
  },
  methods: {
    _getrecommend () {
      getRecommend().then((res) => {
        if (res.code === ERR_OK) {
          this.recommends = res.data.slider
        }
      })
    },
    _getDiscList () {
      getDiscList().then((res) => {
        console.log(res)
      })
    }
  },
  components: {
    Slider
  }
}
</script>

<style lang="stylus" scoped>
@import "../../common/stylus/variable"
.recommend
    position: fixed
    width: 100%
    top: 88px
    bottom: 0
    div
      .slider-wrapper
        position: relative
        width: 100%
        overflow: hidden
      .recommend-list
        .list-title
          height: 65px
          line-height: 65px
          text-align: center
          font-size: $font-size-medium
          color: $color-theme
</style>
