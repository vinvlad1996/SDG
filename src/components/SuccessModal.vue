<template>
  <div class="success">
    <a-modal width="1270px" :footer="null" v-model:open="modalSuccessVisible">
      <h2 class="success__title">Thank You</h2>
      <div class="success__descr">To complete registration, please check your e-mail</div>
    </a-modal>
  </div>
</template>

<script>
import { Modal } from 'ant-design-vue';

export default {
  name: 'SuccessModal',
  components: {
    'a-modal': Modal
  },
  props: {
    visible: Boolean
  },
  data() {
    return {
      modalSuccessVisible: false,
      form: null,
      formData: {
        email: '',
        password: ''
      }
    };
  },
  methods: {
    closeModal() {
      this.modalSuccessVisible = false;
      this.$emit('update:visible', this.modalSuccessVisible);
    },
  }
}
</script>

<style scoped lang="scss">
.success {
  &__title {
    font-size: 77px;
    font-weight: 800;
    line-height: 84.72px;
    letter-spacing: -0.05em;
    text-align: center;
  }

  &__descr {
    margin-top: 20px;
    font-size: 28px;
    font-weight: 700;
    line-height: 38.13px;
    letter-spacing: -0.05em;
    text-align: center;
  }
}
</style>
