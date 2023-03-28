<template>
  <div
    v-bind="$attrs"
    class="bnt"
    @click="hello">
    <slot></slot>
  </div>
</template>

<script>
import { onMounted } from 'vue'

export default {
  inheritAttrs : false,
  props: {
    color: {
      type: String,
      default: 'gray'
    }
  },
  emits: ['hello'],
  mounted() {
    console.log(this.color)
    console.log(this.$attrs)
  },
  setup(props, context) {
  function hello() {
    context.emit('hello')
  }
  onMounted(() => {
    console.log(props.color)
    console.log(context.attrs)
  })
  return{
    hello
  }
}
}
</script>