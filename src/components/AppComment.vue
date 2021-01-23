<template>
  <div>
    <li class="list-item">
      <div>
        <p><strong> {{ mail }} </strong></p>
        <small><slot></slot></small>
      </div>
    </li>
  </div>
</template>

<script>
export default {
  props: {
    mail: String
  }
}
</script>

<style lang="scss" scoped></style>
