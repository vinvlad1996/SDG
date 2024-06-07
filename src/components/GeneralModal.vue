<template>
  <div class="modal">
    <a-modal width="1270px" :footer="null" v-model:open="modalVisible" @cancel="closeModal">
      <div class="modal__container">
        <h2 class="modal__container__title">To register, enter the mail to which our news is sent and set your password</h2>
        <a-form class="modal__container__form" ref="form" @finish="handleSubmit" :model="formData">
          <a-form-item
            name="email"
            :rules="[{ required: true, message: 'Please input your email!' }, { type: 'email', message: 'The input is not a valid email!' }]"
          >
            <a-input class="modal__container__form__input" placeholder="Example@email.com" v-model:value="formData.email" />
          </a-form-item>
          <a-form-item
            name="password"
            :rules="[{ required: true, message: 'Please input your password!' }, { min: 8, message: 'Password must be at least 8 characters!' }]"
          >
            <a-input class="modal__container__form__input" placeholder="Password" type="password" v-model:value="formData.password" />
          </a-form-item>
          <a-form-item>
            <button class="modal__container__form__submit" type="primary" html-type="submit" :disabled="!formIsValid">Submit</button>
          </a-form-item>
        </a-form>
      </div>
    </a-modal>
    <SuccessModal :visible="modalSuccessVisible" @update:visible="modalSuccessVisible = $event" />
  </div>
</template>

<script>
import { Modal, Form, FormItem, Input, message } from 'ant-design-vue';
import axios from 'axios';
import SuccessModal from '@/components/SuccessModal.vue';

export default {
  name: 'GeneralModal',
  components: {
    'SuccessModal': SuccessModal,
    'a-modal': Modal,
    'a-form': Form,
    'a-form-item': FormItem,
    'a-input': Input
  },
  props: {
    visible: Boolean
  },
  data() {
    return {
      modalVisible: false,
      modalSuccessVisible: false,
      formData: {
        email: '',
        password: ''
      }
    };
  },
  computed: {
    formIsValid() {
      return this.formData.email && this.formData.password.length >= 8;
    }
  },
  mounted() {
    const token = localStorage.getItem('authToken');
    if (token) {
      this.redirectToAuthorizedZone(token);
    }
  },
  watch: {
    visible(newVal) {
      if (newVal) {
        this.modalVisible = true;
      }
    }
  },
  methods: {
    closeModal() {
      this.modalVisible = false;
      this.$emit('update:visible', this.modalVisible);
    },
    handleSubmit() {
      this.$refs.form.validate()
        .then(() => {
          const authUrl = 'https://api.dating.com/identity';
          const credentials = btoa(`${this.formData.email}:${this.formData.password}`);

          axios.get(authUrl, {
            headers: {
              'Authorization': `Basic ${credentials}`
            }
          })
          .then(response => {
            const token = response.headers['x-token'];
            localStorage.setItem('authToken', token);
            this.redirectToAuthorizedZone(token);
          })
          .catch(() => {
            this.registerUser();
          });
        })
        .catch(() => {
          message.error('Please fill in the form correctly.');
        });
    },
    registerUser() {
      const url = 'https://api.dating.com/identity';
      axios.put(url, this.formData, {
        headers: {
          'Content-Type': 'application/json'
        }
      })
      .then(response => {
        const token = response.headers['x-token'];
        localStorage.setItem('authToken', token);
        this.modalSuccessVisible = true;
        this.formData.email = '';
        this.formData.password = '';
        this.closeModal();
        this.redirectToAuthorizedZone(token);
      })
      .catch(error => {
        if (error.response) {
          console.error('Response error:', error.response.data);
          console.error('Response status:', error.response.status);
          console.error('Response headers:', error.response.headers);
        } else if (error.request) {
          console.error('Request error:', error.request);
        } else {
          console.error('Error message:', error.message);
        }
        message.error('Registration error. Please try again.');
      });
    },
    redirectToAuthorizedZone(token) {
      window.location.href = `https://www.dating.com/people/#token=${token}`;
    }
  }
}
</script>

<style scoped lang="scss">
.modal {
  &__container {
    text-align: center;
    max-width: 620px;
    margin: 0 auto;
    padding: 130px 20px;

    @media (max-width: 600px) {
      padding: 72px 20px;
    }

    &__title {
      font-size: 24px;
      font-weight: 700;
      line-height: 28px;
      letter-spacing: -0.04em;
    }

    &__form {
      &__input {
        margin-top: 20px;
        border: none;
        border-bottom: 1px solid #d9d9d9;
        border-radius: 0;
        box-shadow: none;
        text-align: center;

        font-size: 18px;
        line-height: 24px;
      }

      &__submit {
        margin-top: 10px;
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
</style>
