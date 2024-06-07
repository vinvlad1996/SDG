<template>
  <div class="general">
    <img class="general__image" alt="general" src="@/assets/general-picture.webp">
    <div class="general__text">
      <h1 class="general__text__title">How to Participate</h1>
      <ol class="general__text__list">
        <li class="general__text__list__item">Subscribe to our News</li>
        <li class="general__text__list__item">
          <button class="general__text__list__item__button" @click="showModal">Sign Up</button>
        </li>
        <li class="general__text__list__item">Check your email inbox </li>
        <li class="general__text__list__item">Wait till September 22</li>
      </ol>
    </div>
    <GeneralModal :visible="modalVisible" @update:visible="modalVisible = $event" />
  </div>
</template>

<script>
import GeneralModal from '@/components/GeneralModal.vue';
export default {
  name: 'GeneralComponent',
  components: {
    'GeneralModal': GeneralModal
  },
  data() {
    return {
      modalVisible: false
    };
  },
  methods: {
    showModal() {
      this.modalVisible = true;
    },
  }
}
</script>

<style scoped lang="scss">
.general {
  display: flex;
  align-items: center;
  justify-content: center;
  column-gap: 100px;
  padding: 90px 20px;

  @media (max-width: 1400px) {
    flex-direction: column;
  }

  &__image {
    @media (max-width: 1400px) {
      max-width: 476px;
    }

    @media (max-width: 600px) {
      max-width: 290px;
    }
  }

  &__text {
    max-width: 476px;

    &__title {
      font-size: 77px;
      font-weight: 800;
      line-height: 84.72px;
      letter-spacing: -0.05em;
      text-align: left;
      background: linear-gradient(145.08deg, #E61726 12.35%, #D4208C 83.63%);
      -webkit-background-clip: text;
      color: transparent;

      @media (max-width: 600px) {
        font-size: 35px;
        line-height: 38.51px;
      }
    }

    &__list {
      padding: 0;
      display: flex;
      gap: 30px;
      flex-direction: column;
      list-style-type: none;
      counter-reset: list-counter;

      @media (max-width: 600px) {
        gap: 22px;
      }

      &__item {
        font-size: 38px;
        font-weight: 600;
        line-height: 75.31px;
        letter-spacing: -0.05em;
        text-align: left;
        position: relative;
        padding-left: 40px;

        @media (max-width: 600px) {
          font-size: 18.82px;
          line-height: 37.3px;
        }

        &::before {
          content: counter(list-counter) ". ";
          counter-increment: list-counter;
          position: absolute;
          left: 0;
          top: 0;
          font-weight: 800;
          background: linear-gradient(238.08deg, #D4208C 0.42%, #E61726 82.5%);
          -webkit-background-clip: text;
          color: transparent;
          font-size: 38px;
        }

        &__button {
          width: 100%;
          max-width: 387px;
          cursor: pointer;
          border-radius: 10px;
          border: none;
          padding: 24px 51px;
          background: linear-gradient(238.08deg, #D4208C 0.42%, #E61726 82.5%);

          font-size: 23px;
          font-weight: 800;
          font-family: Open Sans;
          line-height: 31.32px;
          letter-spacing: 0.03em;
          color: #ffffff;
          text-transform: uppercase;

          @media (max-width: 600px) {
            font-size: 13.81px;
            line-height: 18.81px;
            padding: 15px 0;
          }
        }
      }
    }
  }
}
</style>
