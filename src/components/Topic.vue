<template>
  <div class="box">{{ topic }}</div>
</template>

<script>
export default {
  name: 'Topic',
  props: {
    topic: String
  }
}
</script>

<style lang="scss" scoped>
  .box {
    width: 13rem;
    height: 6rem;
    background-color: #1E000E;
    border-radius: 1rem;
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
    font-size: 1.3rem;
  }
</style>