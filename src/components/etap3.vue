<template>
  <div class="container" v-bind:class="{ hide: hideBox }">
    <div class="title" v-if="!sendSucced && !loading && !error">Weź udział w głosowaniu!</div>
    <div class="row" v-if="!sendSucced && !loading && !error">
      <vote class="vote" @clicked="clicked" v-for="item in array" :key="item._id" :name="item.name" :id="item._id" :votes="item.counter"/>
    </div>
    <div class="send" v-if="sendSucced && !error">
      Dziękujemy za oddanie głosu!
    </div>
    <div class="send" v-if="error">
      Głos z tego adresu już został policzony!!!
    </div>
    <div class="send" v-if="loading">
      <Loading/>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

import vote from '@/components/vote'
import Loading from '@/components/LoadingCircle'

export default {
  name: 'etap3',
  components: {
    vote,
    Loading
  },
  data() {
    return {
      sendSucced: false,
      error: '',
      loading: false,
      array: []
    }
  },
  methods: {
    clicked(id) {
      this.loading = true;
      axios({
        method: 'post',
        url: 'https://golden-lips.herokuapp.com/vote',
        data: {
          "id": id
        }
      }).then(() => {
        this.loading = false;
        this.sendSucced = true;
      }).catch(() => {
        this.loading = false;
        this.error = true;
      });
    }
  },
  created() {
    axios({
      method: 'post',
      url: 'https://golden-lips.herokuapp.com/votelist'
    }).then(response => {
      this.array = response.data.votes;
    });
  },
  computed: {
    hideBox() {
      if(this.sendSucced || this.error) {
          return true;
      }
      return false;
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  background-color: #DDAB40;
  color: #1E000E;
  font-family: Lato;
  width: 100%;
  height: 25rem;
  display: flex;
  flex-direction: column;
  padding-bottom: 4rem;
  align-items: center;
  justify-content: center;
  @media (max-width: 768px) {
    height: auto;
  }

  .title {
    width: 60rem;
    height: 5rem;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
    margin-bottom: 3rem;
    font-weight: 700;
    @media (max-width: 768px) {
      width: 100%;
      font-size: 1.6rem;
      margin-top: 2rem;
    }
  }

  .row {
    width: 60rem;
    height: auto;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: auto;
    grid-row-gap: 2.7rem;
    @media (max-width: 768px) {
      width: 100%;
      grid-template-columns: 1fr;
      grid-template-rows: auto;
    }

    .vote {
      place-self: center;
    }
  }

  .send {
    width: 60rem;
    height: 29rem;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 3rem;
    @media (max-width: 768px) {
      width: 90%;
      font-size: 2rem;
      line-height: 3rem;
    }
  }
}

.hide {
    animation: hide 4s forwards;
}

@keyframes hide {
    0% {
        height: 25rem;
    }
    90% {
        height: 25rem;
        opacity: 1;
    }
    100% {
        height: 0rem;
        visibility: hidden;
        opacity: 0;
    }
}

</style>