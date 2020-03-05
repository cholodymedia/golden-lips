<template>
  <div class="container">
    <div class="banner">
      <div class="left">
        <div class="box">
          <div class="top">
            <div class="link">Wiśniowa</div>
            <div class="link">Kontakt</div>
          </div>
          <div class="middle"></div>
        </div>
      </div>
      <div class="right">
        <img :src="image" alt="logo">
      </div>
    </div>

    <div class="info">
      <div class="box">
        <question title="Gdzie i kiedy?" text="Konkurs odbędzie się w czytelni koło biblioteki; termin konkursu zostanie podany póżniej"/>
        <question title="Kto organizuje?" text="Organizatorami konkursu są: Sylwia Błażejewska oraz Beata Walczak"/>  
        <question title="Kto może wziąć udział?" text="W konkursie mogą wziać udział wszyscy uczniowie z naszej szkoły"/>  
        <question title="Czy będą jakieś nagrody?" text="Zobaczymy"/>  
        <question title="Gdzie szukać więcej informacji?" text="Na tej stronie będą zamieszczane wszelkie niezbędne informacje dla zainteresowanych. Jeśli jednak wolisz bardziej werbalne środki przekazu, to panie z biblioteki mogą udzielić takich informacji"/>
      </div>
    </div>

  </div>
</template>

<script>
import image from '@/assets/logo.png';
import question from '@/components/Question';

export default {
  name: 'Start',
  components: {
    question
  },
  data() {
    return {
      image: image
    }
  }
}
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css?family=Lato&display=swap');
  .container{
    width: 100vw;
    display: flex;
    flex-direction: column;
    font-family: 'Lato', sans-serif;
    color: #e3dac9c0;
    overflow-x: hidden;

    .banner {
      width: 100%;
      height: 100vh;
      display: flex;
      flex-direction: row;
      background-color: white;

      .left {
        flex: 3;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;

        .box {
          width: 75%;
          height: 80%;
        }
      }

      .right {
        flex: 2.5;
        display: flex;
        justify-content: flex-start;
        align-items: center;

        img {
          width: 28rem;
        }
      }
      
      }
      .bottom{
        width: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin-top: auto;
        font-size: 1.5rem;
        color: white;
        text-transform: uppercase;
        padding-bottom: 4rem;

        p{
          margin: 0;
          padding: 0.2rem;
        }
      }
    .info{
      background-color: #1E000E;
      min-height: 100vh;
      width: 100vw;
      display: flex;
      flex-direction: column;
      align-items: center;

      .box{
        width: 50vw;
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        padding-bottom: 9vh;
      }
    }
  }

</style>