<template>
  <div class="my-counter">
    <button
      type="button"
      class="btn btn-light"
      :disabled="obj.goods_count == 1"
      @click="obj.goods_count--"
    >
      -
    </button>
    <input
      type="number"
      class="form-control inp"
      v-model.number="obj.goods_count"
    />
    <button type="button" class="btn btn-light" @click="obj.goods_count++">
      +
    </button>
  </div>
</template>

<script>
export default {
  props: {
    obj: Object, // 商品对象
  },
  watch: {
    obj: {
      deep: true,
      handler() { // 监听商品数量，小于1则强制修改数量为1
        if (this.obj.goods_count < 1) {
          this.obj.goods_count = 1
        }
      },
    },
  },
}
</script>

<style lang="less" scoped>
.my-counter {
  display: flex;
  .inp {
    width: 45px;
    text-align: center;
    margin: 0 10px;
    padding: 0;
  }
  .btn,
  .inp {
    transform: scale(0.9);
  }
}
</style>
