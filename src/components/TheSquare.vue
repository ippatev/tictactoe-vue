<template>
  <button class="square" @click="$emit('onClick')">
    {{ value }}
  </button>
</template>
<script>
export default {
  props: ['value'],
  /* emits not supported for vue 2
  emits: ['onClick'],
   */
  /* TODO write component with functional style.
  functional: true,
  render(h, {props}) {
    return (
        <button class="square" onClick={props.onClick}>
          { props.value }
        </button>
    )
  },
   */
}
</script>
