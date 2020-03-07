<template>
  <div class="question"> 
    <p class="question_title">{{ title }}</p>
    <p class="question_text"> {{ text }}</p>
  </div>
</template>

<script>
export default {
  name: "Question",
  props: {
    title: String,
    text: String
  }
}
</script>

<style lang="scss" scoped>
  p {
    margin: 0;
    padding: 0;
  }
  .question {
    width: 90%;
  }
  .question_title {
    text-transform: uppercase;
    color: #1E000E;
    font-size: 2rem;
    padding-top: 9vh;
    font-weight: 900;
    z-index: 1;

    &::before {
      content: '';
      width: 20rem;
      height: 3rem;
      background-color: #DDAB40;
      position: absolute;
      z-index: -1;
      transform: translate(0rem, -1rem)
    }
  }
  .question_text {
     font-size: 1.3rem;
     padding-top: 1.5vh;
     line-height: 1.6rem;
     color: #707070;
     line-height: 2rem;
  }
</style>