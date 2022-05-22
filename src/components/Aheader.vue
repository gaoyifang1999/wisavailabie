<template >
  <div class="wrapper">
    <slot />
  </div>
</template>

<script>
export default {
  name: 'AHeader'
}
</script>

<style lang="less" scoped>
  .wrapper {
    width: 100%;
    // height: 100px;
    background-color: antiquewhite;
  }
</style>
