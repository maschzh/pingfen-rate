
<template>
  <div class="smd-rate">
    <i
      class="iconfont icon-xingxingshixin"
      v-for="(item,index) in 5"
      :key="index+item"
      @click="disabled?'':choice(index)"
      :class="isChoice(index)"
    >
      <i
        v-if="disabled&&index==Math.floor(childScore)"
        class="iconfont icon-xingxingshixin icon-star floor"
        :style="'width:'+width"
      ></i>
    </i>
  </div>
</template>

<script>
export default {
  props: {
    score: { // 评分数值
      type: Number,
      default: 0
    },
    disabled: { // 是否禁用评分选择  默认是false 即可以进行评分
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      childScore: this.score // 避免直接修改props的值，将props的评分数值保存在当前组件管理的data中
    }
  },

  watch: {
    score (nv) { // 监听props的值 将变化的值赋值给变量
      this.childScore = nv
    }
  },
  computed: {
    width () {// 最后那个星的百分数
      let width = Number(this.childScore * 100 - Math.floor(this.childScore) * 100) + '%' // 去设置半颗星的宽度
      return width
    }
  },

  mounted () { },

  created () { },

  methods: {
    choice (index) { //点击设置分数
      this.$emit('choice', index + 1)
    },
    isChoice (index) {
      return index + 1 <= this.childScore ? 'icon-star' : 'icon-star-o'
    }
  }

}

</script>
<style lang="less"  rel="stylesheet/less" scope type="text/less">
@import url('./iconfont.css');
@r: 100;
.icon-xingxingshixin {
  font-size: 62rem / @r;
  position: relative;
}
.icon-star {
  color: #ef4034;
}
.icon-star-o {
  color: #ccc;
}
.floor {
  position: absolute;
  left: 0;
  top: -3rem / @r;
  overflow: hidden;
}
</style>