<template>
  <div class="box">
    <div class="class">{{ votes }}</div>
    <div class="name">{{ name.split(" ")[0] }}<br>{{ name.split(" ")[1] }}</div>
    <div class="button-box">
      <div class="button" @click="clickButton">Głosuj</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    id: String,
    votes: Number
  },
  methods: {
    clickButton() {
      this.$emit('clicked', this.id);
    }
  }
}
</script>

<style lang="scss" scoped>
.box {
  width: 16rem;
  height: 12rem;
  background-color: #1E000E;
  position: relative;
  display: flex;
  flex-direction: column;
  &:hover > .button-box {
    animation: appear 0.3s forwards;
  }
  &:hover > .name {
    transform: translateY(1rem);
  }
  .class {
    position: absolute;
    right: 1rem;
    top: 1rem;
    color: white;
    font-weight: 700;
  }
  .name {
    flex: 5;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
    color: white;
    font-weight: 700;
    transform: translateY(2rem);
    transition: 0.3s;
    line-height: 2.8rem;
    margin-left: -1.5rem;
  }
  .button-box {
    flex: 3;
    display: flex;
    justify-content: center;
    align-items: center;
    animation: disappear 0.3s forwards;
    opacity: 0;

    .button {
      width: 8rem;
      height: 2.5rem;
      background-color: white;
      border-radius: 2rem;
      display: flex;
      justify-content: center;
      align-items: center;
      text-transform: uppercase;
      font-weight: 700;
      font-size: 0.85rem;
      cursor: pointer;
    }
  }
}

@keyframes appear {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@keyframes disappear {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}
</style>