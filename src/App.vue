<template>
  <div>
    <MyHeader backgroundColor="violet" title="购物车案例"></MyHeader>
    <div class="main">
      <MyGoods v-for="obj in list" :key="obj.id" :gObj="obj"></MyGoods>
    </div>
    <MyFooter @changeAll="allFn" :arr="list"></MyFooter>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue'
import MyGoods from './components/MyGoods.vue'
import MyFooter from './components/MyFooter.vue'
export default {
  data() {
    return {
      list: [], // 保存商品信息
    }
  },
  created() {
    // console.log(this)
    this.$axios({
      url: '/api/cart',
    }).then((res) => {
      // console.log(res)
      this.list = res.data.list
    })
  },
  methods: {
    allFn(bool) {
      // 把MyFooter内的全选状态true/false同步给所有小选框的关联属性上
      this.list.forEach((obj) => obj.goods_state = bool)
    },
  },
  components: {
    MyHeader,
    MyGoods,
    MyFooter,
  },
}
</script>
<style scoped>
.main {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>
