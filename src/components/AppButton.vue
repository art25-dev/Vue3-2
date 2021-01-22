<template>
  <button class="btn primary" @click="$emit('action')">
    <slot></slot>
  </button>
</template>

<script>
export default {
  emits: ['action'],
  props: {}
}
</script>

<style lang="scss" scoped></style>
