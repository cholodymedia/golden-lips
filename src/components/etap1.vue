<template>
    
    <div id="container">
    <div id="box">
        <div id="title">
            Wyślij swoją propozycję tematu
        </div>
        <div id="text">
            Zbieramy propozycje tematów na najbliższą edycję konkursu. Jeśli chcesz, możesz dodać swoją propozycję poniżej:
        </div>
        <div id="form" v-if="!sended">
            <form>
            <div id="subject">
                <input type="text" v-model="topic" maxlength="30" placeholder="Wpisz swoją propozycję...">
            </div>
            <br>
            <div id="send">
                <button @click="send">Wyślij</button>
            </div>
            </form>
        </div>
        <div class="send" v-if="sended">
            Wysłano propozycję tematu!
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
                url: 'http:/golden-lips-server.herokuapp.com/topic/send',
                data: {
                    
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
        width: 100vw;
        display: flex;
        flex-direction: column;
        align-items: center;
        font-family: "Lato";
        text-transform:uppercase;
        background-color: #1e000e;
        padding-bottom: 2rem;

        #box {
            width:  50vw;
            display: flex;
            flex-direction: column;
            justify-content: center;

        #title {
            height: 5rem;
            font-size: 2rem;
            color:rgb(235, 181, 33);
            display:flex;
            justify-content: flex-start;
            align-items: center;
            font-weight: 900;
        }

        #text {
            color:#e3dac9c0;
            height: 8rem;
            font-size: 1.3rem;
            display: flex;
            justify-content: flex-start;
            align-items: center;
        }

        .send {
            width: 100%;
            height: 20vh;
            display: flex;
            align-items: center;
            color:rgb(235, 181, 33);
            font-size: 1.5rem;
        }

        #form {
            display:flex;
            justify-content: flex-start;
            align-items: center;
            height: 20vh;

                #subject {
                    width: 20rem;
                    height: 2rem;
                    border-radius: 10px;
                    background-color: #110008;
                    
                        input {
                            margin: 0;
                            padding: 0;
                            padding-left:0.5rem;
                            border: none;
                            outline: none;
                            width:100%;
                            height: 100%;
                            background:none;
                            font-size:1.2rem;
                            font-family: "Lato";
                            color:#e3dac9c0;
                        }
                    }
                #send {
                    button {
                    margin-top:3vh;
                    width: 8rem;
                    height: 2.5rem;
                    border-radius: 10px;
                    font-size: 1.2rem;
                    font-weight: 900;
                    font-family:"Lato";
                    border:none;
                    outline:none;
                    background-color: rgb(235, 181, 33);
                    color:#1e000e;
                    
                    }
                }
                
            }
        }
    }
</style>