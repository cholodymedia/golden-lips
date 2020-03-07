<template>
  <div id="app">
    <Start/>
    <etap1/>
    <!-- <etap2/> -->
    <!-- <etap3/> -->
  </div>
</template>

<script>
import Start from "@/components/Start.vue"
import etap1 from "@/components/etap1"
// import etap2 from "@/components/etap2"
// import etap3 from "@/components/etap3"


export default {
  name: 'app',
  components: {
    Start,
    etap1,
    // etap2,
    // etap3
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Lato:300,400,500,600&display=swap');

body, html {
  margin: 0;
  padding: 0;
  font-family: Lato;
}

#app {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
  overflow-x: hidden;
}
</style>
