<template>
  <div class="bottom-bar">
    <CheckButton class="select-all"
                 :is-checked="isSellectAll" @click.native="checkClick"></CheckButton>
    <span class="select-all-text">全选</span>
    <span class="total-price">合计: ¥{{totalPrice}}</span>
    <span class="buy-product">去计算({{cartLength}})</span>
  </div>
</template>

<script>
import CheckButton from "components/content/bakcTop/checkButton/CheckButton";
import { mapGetters } from 'vuex';

export default {
  name: "CartBottomBar",
  components: {
    CheckButton
  },
  computed: {
    ...mapGetters(['cartList']),
    totalPrice() {
      return this.cartList.filter(item => {
        return item.checked
      }).reduce((preValue, item) => {
        return preValue + item.price * item.count
      },0).toFixed(2)
    },
    cartLength() {
      return this.cartList.filter(item => item.checked).length
    },
    isSellectAll(){
      if(this.cartList.length === 0) return false
      // return !(this.cartList.filter(item => !item.checked).length)
      // return !this.cartList.find(item => !item.checked)
      for(let item of this.cartList){
        if(!item.checked) {
          return false
        }
      }
      return true
    }
  },
  methods: {
    checkClick(){
     if(this.isSellectAll) {
        //全部选中
        this.cartList.forEach(item => item.checked = false)
      }else{
        //部分或全部不选中
        this.cartList.forEach(item => item.checked = true)
      }
    }
  }
}
</script>

<style scoped>
.bottom-bar {
  width: 100%;
  height: 40px;
  background-color: #eee;
  position: fixed;
  bottom: 49px;
  left: 0;
  box-shadow: 0 -2px 3px rgba(0, 0, 0, .2);
  font-size: 12px;
  color: #888;
  line-height: 40px;
  padding-left: 35px;
  box-sizing: border-box;
}

.bottom-bar .select-all {
  position: absolute;
  line-height: 0;
  left: 12px;
  top: 10px;
}

.bottom-bar .select-all-text{
  float: left;
}

.bottom-bar .total-price {
  margin-left: 15px;
  font-size: 16px;
  color: #666;
}

.bottom-bar .buy-product {
  background-color: orangered;
  color: #fff;
  width: 100px;
  height: 40px;
  text-align: center;
  line-height: 40px;
  float: right;
}
</style>
