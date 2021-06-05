<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll';

export default {
  name: "Scroll",
  props: {
    probeType: {
      type: Number,
      default: 0
    },
    pullUpLoad: {
      type: Boolean,
      default: false
    }
  },
  //保存变量
  data() {
    return {
      scroll: null
    }
  },

  //生命周期函数
  mounted() {
    //1.创建BScroll对象
    this.scroll = new BScroll(this.$refs.wrapper, {
      click: true, //加上这个组件里面就可以切换点击
      probeType: this.probeType,  //probeType不能写死为3，因为有的页面需要实时监听，有的页面不需要实时监听，去上面创建一个props让它默认为0，就可以根据传入的值决定要不要监听。
      pullUpLoad: this.pullUpLoad
    })

    //2.监听滚动的位置
    if(this.probeType === 2 || this.probeType === 3) {
      this.scroll.on('scroll', (position) => {
        //console.log(position)
        this.$emit('scroll', position)// position不是在这个scroll组件中用的，也不需要用它，谁需要就把position传给谁；通过自定义事件scroll用$emit传出去。
      })
    }

    //3.监听scroll滚动到底部
    if(this.pullUpLoad) {
      this.scroll.on('pullingUp', () => {
        this.$emit('pullingUp')
      })
    }
  },
  methods: {
    scrollTo(x, y, time=500) {
      this.scroll && this.scroll.scrollTo && this.scroll.scrollTo(x, y, time)
    },
    refresh() {
      this.scroll && this.scroll.refresh && this.scroll.refresh()
    },
    finishPullUp() {
      this.scroll && this.scroll.finishPullUp()
    },
    getScrollY() {
      return this.scroll ? this.scroll.y : 0
    }
  }
}
</script>

<style scoped>
  .wrapper{
    overflow: hidden;
  }
</style>
