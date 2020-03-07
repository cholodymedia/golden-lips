<template>
    
    <div id="container">
        <div id="box">
            <div id="title">
                Wyślij swoją propozycję tematu
            </div>
            <div id="text">
                Zbieramy propozycje tematów na najbliższą edycję konkursu. Jeśli chcesz, możesz dodać swoją propozycję poniżej:
            </div>
            <div class="form" v-if="!sended">
                <div class="subject">
                    <input type="text" v-model="topic" maxlength="30" placeholder="Wpisz swoją propozycję...">
                </div>
                <br>
                <div class="send">
                    <button @click="send">wyślij</button>
                </div>
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
            sended: false
        }
    },
    methods: {
        send() {
        event.preventDefault();
            axios({
                method: 'post',
                url: 'http://localhost:5000/topic/add',
                data: {
                    SECRET_KEY: "GOLDEN_LIPS",
                    topic: this.topic
                }
            });
            this.topic = ''
            this.sended = true;
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

        #title {
            height: 5rem;
            font-size: 2rem;
            color:#1E000E;
            display:flex;
            justify-content: flex-start;
            align-items: center;
            font-weight: 900;
        }

        #text {
            color:#464646;
            height: 7rem;
            font-size: 1.3rem;
            display: flex;
            justify-content: flex-start;
            align-items: center;
            line-height: 2rem;
        }

        .form {
            width: 100%;
            height: 4rem;
            display: flex;
            flex-direction: row;
            margin-top: 1rem;

            .subject {
                width: auto;
                height: 100%;
                display: flex;
                justify-content: flex-start;
                align-items: center;

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
                }
            }
        }
    }
}
</style>