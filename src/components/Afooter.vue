<template >
  <div class="wrapper"> <slot /></div>
</template>

<script>
export default {
  name: 'AFooter'
}
</script>

<style lang="less" scoped>
  .wrapper {
    width: 100%;
    // height: 100px;
    background-color: rgb(224, 224, 224);
  }
</style>
