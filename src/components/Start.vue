<template>
  <div class="container">
    <div class="banner">
      <div class="left">
        <div class="box">
          <div class="top">
            <div class="link">Wiśniowa</div>
            <div class="link">Kontakt</div>
          </div>
          <div class="middle">
            <div class="title">ZŁOTE USTA</div>
            <div class="subtitle">KONKURS RECYTATORSKI NA WIŚNIOWEJ</div>
            <div class="info-text">BILIOTEKA SZKOLNA ZACHĘCA DO WZIĘCIA UDZIAŁU W IGRZYSKACH NA MIKOROFONY, GDZIE ZWYCIEZCA MOŻE BYĆ TYLKO JEDEN.</div>
            <div class="button-box">
              <button>więcej</button>
            </div>
          </div>
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
  .container{
    width: 100%;
    display: flex;
    flex-direction: column;
    font-family: 'Lato', sans-serif;
    color: #e3dac9c0;

    .banner {
      width: 100%;
      height: 100vh;
      display: flex;
      flex-direction: row;
      background-color: white;
      z-index: 1;

      .left {
        flex: 3.5;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;

        .box {
          width: 38rem;
          height: 85%;
          display: flex;
          flex-direction: column;

          .top {
            width: 100%;
            height: 4rem;
            display: flex;
            flex-direction: row;

            .link {
              width: 12rem;
              height: 100%;
              display: flex;
              align-items: center;
              color: black;
              font-weight: 200;
              font-size: 1.4rem;
            }
          }

          .middle {
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;

            .title {
              width: 100%;
              height: 6rem;
              font-size: 5rem;
              font-weight: 900;
              color: #1E000E;
            }
            .subtitle {
              width: 100%;
              height: 5rem;
              display: flex;
              font-size: 1.45rem;
              font-weight: 500;
              color: black; 
              align-items: center;
              z-index: 1;
              &::before {
                content: '';
                width: 7.7rem;
                height: 1.2rem;
                background-color: #DDAB40;
                position: absolute;
                z-index: -1;
                transform: translate(0.5rem, 0.45rem)
              }
            }
            .info-text {
              width: 92%;
              height: 7rem;
              display: flex;
              font-size: 1.3rem;
              line-height: 1.6rem;
              font-weight: 400;
              color: #707070; 
              align-items: center;
              z-index: 1;
              &::before {
                content: '';
                width: 7.7rem;
                height: 1.2rem;
                display: flex;
                background-color: #DDAB40;
                position: absolute;
                z-index: -1;
                transform: translate(24.3rem, 0.5rem)
              }
            }
            .button-box {
              width: 100%;
              height: 7rem;
              display: flex;
              align-items: center;

              button {
                width: 8rem;
                height: 2.5rem;
                background-color: #DDAB40;
                border: none;
                font-size: 1.2rem;
                font-family: Lato;
                border-radius: 0.8rem;
                outline: none;
                z-index: 1;
                transition: 0.2s;

                &:hover {
                  transform: translate(0.38rem, 0.35rem);
                  cursor: pointer;
                }
              }
              &::before {
                content: '';
                width: 7.7rem;
                height: 2.1rem;
                border: 2px solid black;
                border-radius: 0.8rem;
                position: absolute;
                z-index: 0;
                transform: translate(0.45rem, 0.37rem)
              }
            }
          }
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
      min-height: 100vh;
      width: 100%;
      display: flex;
      flex-direction: column;
      align-items: center;

      .box{
        width: 50rem;
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        padding-bottom: 9vh;
      }
    }
  }

</style>