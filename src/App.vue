<template>
  <div id="app">
    <Start/>
    <etap1 v-if="menageState.etap1"/>
    <etap2 v-if="menageState.etap2"/>
    <etap3 v-if="menageState.etap3"/>
  </div>
</template>

<script>
import axios from 'axios'

import Start from "@/components/Start.vue"
import etap1 from "@/components/etap1"
import etap2 from "@/components/etap2"
import etap3 from "@/components/etap3"


export default {
  name: 'app',
  data() {
    return {
      menageState: null,
      error: null
    }
  },
  components: {
    Start,
    etap1,
    etap2,
    etap3,
  },
  created() {
    axios({
        method: "POST",
        url: "https://graphql.datocms.com",
        headers: {
          Authorization: 'bearer ' + '2d0c7c7c56e6cdfc216c7e568b86b4'
        },
        data: {
          query: `
            {
              menageState {
                etap1
                etap2
                etap3
              }
            }
          `
        }
      }).then(result => {
        this.menageState = result.data.data.menageState
      }).catch(err => {
        this.error = err;
      })
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Lato:300,400,500,600&display=swap');

body, html {
  margin: 0;
  padding: 0;
  font-family: Lato;
  scroll-behavior: smooth;
}

#app {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
  overflow-x: hidden;
}
</style>
