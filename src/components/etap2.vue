<template>
  <div class="container" v-bind:class="{ hide: hideBox }">
    <div class="application" v-if="!sended && !sending && !error">
      <div class="title">
        Chcę wziąć udział
      </div>
      <div class="main">
        <div class="left">
          <div class="single-name">
            Imię
          </div>
          <div class="single-name">
            Nazwisko
          </div>
          <div class="single-name">
            Klasa
          </div>
          <div class="single-name">
            Temat
          </div>
          <div class="single-name">
            Email
          </div>
          </div>
        <div class="right">
          <div class="single-input"><input type="text" v-model="imie" required></div>
          <div class="single-input"><input type="text" v-model="nazwisko" required></div>
          <div class="single-input"><input type="text" v-model="klasa" required></div>
          <div class="single-input">
            <select v-model="temat" required>
              <option selected disabled></option>
              <option v-for="topic in topics" :key="topic._id">{{ topic.topic }}</option>
            </select>
          </div>
          <div class="single-input"><input type="email" v-model="email" required></div>
        </div>
      </div>
      <div class="button">
        <button @click="send">Zapisz się!</button>
      </div>
    </div>
    <div class="info-box" v-if="sended || error || sending">
      <div class="info" v-if="sended">
        Twoje zgłoszenie zostało przesłane. Dziękujemy ; )
      </div>
      <div class="info" v-if="error">
          Błąd Servera. Przepraszamy ale chwilowo nie możemy przesłać twojego zgłoszenia : (
          <p class="admin">Powiadom admina => <a href="mailto:cholodymedia@gmail.com">cholodymedia@gmail.com</a></p>
      </div>
      <div class="info circle" v-if="sending">
          <div class="lds-ring"><div></div><div></div><div></div><div></div></div>
          <p>Wysyłanie zgłoszenia</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: "etap2",
  data() {
    return {
      imie: '',
      nazwisko: '',
      klasa: '',
      temat: '',
      email: '',
      topics: [],
      error: '',
      sended: false,
      sending: false
    }
  },
  created() {
    axios({
      method: 'post',
      headers: {
        "Content-Type": "application/x-www-form-urlencoded",
        Accept: "application/json"
      },
      url: 'http://192.168.1.37:5000/listselected'
    }).then(data => {
      this.topics = data.data.selected
    }).catch(err => {
      this.error = err
    })
  },
  methods: {
    send() {
    event.preventDefault();
      if(this.imie != '' && this.nazwisko != '' && this.klasa != '' && this.temat != '' && this.email != '') {
        this.sending = true;
        axios({
          method: 'post',
          url: 'http://192.168.1.37:5000/application',
          data: {
              temat: this.temat,
              imie: this.imie,
              nazwisko: this.nazwisko,
              klasa: this.klasa,
              email: this.email
          }
        }).then(() => {
          this.sending = false;
          this.sended = true;
        }).catch(err => {
          this.sending = false;
          this.error = err
        })
      }else {
        alert('Uzupełnij wszyskie pola!')
      }
    }
  },
  computed: {
    hideBox() {
        if(this.sended) {
            return true;
        }
        return false;
    }
  }
}
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css?family=Lato:400,700,900&display=swap');


  .container {
    background-color: #DDAB40;
    color: #1E000E;
    font-family: Lato;
    width: 100%;
    height: 28rem;
    display: flex;
    flex-direction: row;
    align-items: center;
    font-weight: 900;
    padding-bottom: 4rem;
    @media (max-width: 768px) {
      justify-content: center;
    }

    .info-box {
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      @media (max-width: 768px) {
        width: 88%;
      }
    }

    .info {
      font-size: 1.5rem;
      font-weight: 500;
      text-transform: none;
      color:#1E000E;
      line-height: 2.5rem;

      .admin {
        font-size: 1.1rem;
        font-weight: 500;
        text-transform: none;
        color: rgb(105, 12, 12);
      }
    }

    .circle {
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      color: white;
    }

    .application {
      width: 100%;
      height: 100%;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .title {
      width: 100%;
      height: 6rem;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 40px;
      margin-top: 1rem;
      text-transform: uppercase;
      @media (max-width: 768px) {
        width: 90%;
        height: 5rem;
        font-size: 1.7rem;
        margin-top: 2.5rem;
      }
    }
    .main {
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: row;
      width: 30rem;
      height: 18rem;
      @media (max-width: 768px) {
        width: 90%;
        height: 17rem;
        margin-top: 2rem;
      }

      .left {
        width: 30%;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        @media (max-width: 768px) {
          width: 20%;
        }

        .single-name {
          width: 8rem;
          height: 3rem;
          justify-content: flex-start;
          display: flex;
          align-items: center;
          font-size: 1.2rem;
          @media (max-width: 768px) {
            width: 100%;
            height: 3.5rem;
          }
        }
      }
      .right {
        width: 70%;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        @media (max-width: 768px) {
          width: 80%;
        }

        .single-input {
          width: 20rem;
          height: 3rem;
          display: flex;
          justify-content: flex-end;
          align-items: center;
          @media (max-width: 768px) {
            width: 100%;
            height: 3.5rem;
          }
          input {
            border-radius: 0.7rem;
            background-color: #AF811F;
            border: none;
            width: 15rem;
            height: 1.8rem;
            color: white;
            font-size: 1.1rem;
            outline: none;
            padding-left: 1rem;
            @media (max-width: 768px) {
              width: 13rem;
            }
          }
          select {
            border-radius: 0.7rem;
            background-color: #AF811F;
            border: none;
            width: 16rem;
            height: 2rem;
            color: white;
            font-size: 1.3rem;
            outline: none;
            -moz-appearance: none; /* Firefox */
            -webkit-appearance: none; /* Safari and Chrome */
            appearance: none;
            cursor: pointer;
            padding-left: 1rem;
            @media (max-width: 768px) {
              width: 14rem;
            }
          }
        }
      }
    }
    .button {
      display: flex;
      width: 30rem;
      justify-content: flex-end;
      @media (max-width: 768px) {
        width: 100%;
        height: 4rem;
        justify-content: center;
        align-items: center;
        margin-top: 2rem;
      }
      
      button {
        border-radius: 0.5rem;
        background-color: #1E000E;
        border: none;
        color: white;
        font-family: Lato;
        font-weight: 900;
        text-transform: uppercase;
        width: 16rem;
        height: 2.5rem;
        font-size: 1rem;
        outline: none;
        margin-right: 0.5rem;
        @media (max-width: 768px) {
          width: 12rem;
          height: 3rem;
        }
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


.lds-ring {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-ring div {
  box-sizing: border-box;
  display: block;
  position: absolute;
  width: 64px;
  height: 64px;
  margin: 8px;
  border: 8px solid #fff;
  border-radius: 50%;
  animation: lds-ring 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  border-color: #fff transparent transparent transparent;
}
.lds-ring div:nth-child(1) {
  animation-delay: -0.45s;
}
.lds-ring div:nth-child(2) {
  animation-delay: -0.3s;
}
.lds-ring div:nth-child(3) {
  animation-delay: -0.15s;
}
@keyframes lds-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>