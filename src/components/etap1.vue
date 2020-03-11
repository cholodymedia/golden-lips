<template>
    <div id="container" v-bind:class="{ hide: hideBox }">
        <div id="box">
            <div id="title" v-if="!sended && !sending && !error">
                Wyślij swoją propozycję tematu
            </div>
            <div id="text" v-if="!sended && !sending && !error">
                Zbieramy propozycje tematów na najbliższą edycję konkursu. Jeśli chcesz, możesz dodać swoją propozycję poniżej:
            </div>
            <div class="form" v-if="!sended && !sending && !error">
                <div class="subject">
                    <input type="text" v-model="topic" maxlength="30" placeholder="Wpisz swoją propozycję...">
                </div>
                <br>
                <div class="send">
                    <button @click="send">wyślij</button>
                </div>
            </div>
            <div class="info" v-if="sended">
                Propozycja tematu została przesłana. Dziękujemy ; )
            </div>
            <div class="info" v-if="error">
                Błąd Servera. Przepraszamy ale chwilowo nie możemy przesłać twojej propozycji : (
                <p class="admin">Powiadom admina => <a href="mailto:cholodymedia@gmail.com">cholodymedia@gmail.com</a></p>
            </div>
            <div class="info circle" v-if="sending">
                <div class="lds-ring"><div></div><div></div><div></div><div></div></div>
                <p>Wysyłanie propozycji</p>
            </div>
        </div>
    </div>     
</template>

<script>
import axios from 'axios'

export default {
    name:"etap1",
    data() {
        return {
            topic: '',
            sended: false,
            error: '',
            sending: false,
        }
    },
    methods: {
        send() {
            event.preventDefault();
            this.sending = true;
            axios({
                method: 'post',
                url: 'http://localhost:5000/addtopic',
                data: {
                    topic: this.topic
                }
            }).then(() => {
                this.sended = true
                this.sending = false
            }).catch(error => {
                this.sending = false
                this.error = error
            })
            
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

@import url('https://fonts.googleapis.com/css?family=Lato&display=swap');
#container {
    width: 100%;
    height: 25rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    font-family: "Lato";
    text-transform:uppercase;
    background-color: #DDAB40;
    padding-bottom: 2rem;

    #box {
        width:  50rem;
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;

        @media (max-width: 768px) {
          width: 100%;
        }

        .info {
            font-size: 1.5rem;
            font-weight: 500;
            text-transform: none;
            color:#1E000E;
            line-height: 2.5rem;

            @media (max-width: 768px) {
                width: 90%;
                height: 100%;
                display: flex;
                justify-content: center;
                align-items: center;
                text-align: center;
                font-size: 1.5rem;
                font-weight: 700;
                flex-direction: column;
            }

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

        #title {
            height: 5rem;
            font-size: 2rem;
            color:#1E000E;
            display: flex;
            justify-content: flex-start;
            align-items: center;
            font-weight: 900;
            @media (max-width: 768px) {
                font-size: 1.4rem;
                justify-content: center;
                align-items: center;
                width: 80%;
            }
        }

        #text {
            color:#464646;
            height: 7rem;
            font-size: 1.3rem;
            display: flex;
            justify-content: flex-start;
            align-items: center;
            line-height: 2rem;
            @media (max-width: 768px) {
                font-size: 1rem;
                width: 80%;
                height: 9rem;
            }
        }

        .form {
            width: 100%;
            height: 4rem;
            display: flex;
            flex-direction: row;
            margin-top: 1rem;

            @media (max-width: 768px) {
                flex-direction: column;
                height: 6rem;
                margin-top: 1rem;
            }

            .subject {
                width: auto;
                height: 100%;
                display: flex;
                justify-content: flex-start;
                align-items: center;

                @media (max-width: 768px) {
                    justify-content: center;
                }

                input {
                    width: 23rem;
                    height: 2.5rem;
                    background-color: #AF811F;
                    border: none;
                    border-radius: 0.7rem;
                    outline: none;
                    color: white;
                    font-family: Lato;
                    font-size: 1.1rem;
                    padding-left: 2rem;
                    @media (max-width: 768px) {
                        width: 17rem;
                    }
                    &::placeholder {
                        color: white;
                    }
                }
            }
            .send {
                width: 100%;
                height: 100%;
                display: flex;
                justify-content: flex-start;
                align-items: center;
                @media (max-width: 768px) {
                    justify-content: center;
                    margin-top: 0.5rem;
                }

                button {
                    margin-left: 3rem;
                    width: 10rem;
                    height: 2.5rem;
                    background-color: #1E000E;
                    border: none;
                    outline: none;
                    color: white;
                    font-family: Lato;
                    font-size: 1.1rem;
                    border-radius: 0.7rem;
                    transition: 0.1s;

                    @media (max-width: 768px) {
                        margin: 0;
                        width: 12rem;
                        height: 3rem;
                    }
                    
                    &:hover {
                        cursor: pointer;
                        transform: scale(0.96);
                    }
                }
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