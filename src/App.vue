<template>
  <div>
    <GeneralComponent />
  </div>
</template>

<script>
import GeneralComponent from './components/GeneralComponent.vue';

export default {
  name: 'App',
  components: {
    GeneralComponent
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.ant-modal .ant-modal-content {
  border-radius: 50px;
}

.ant-modal .ant-modal-close {
  height: 45px;
  width: 45px;
}

.ant-modal .ant-modal-close-x {
  font-size: 29px;
  position: relative;
  width: 29px;
  height: 29px;

  &::after {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    width: 29px;
    height: 4px;
    background: linear-gradient(238.08deg, #D4208C 0.42%, #E61726 82.5%);
    transform: translate(-50%, -50%);
    transform: translate(-50%, -50%) rotate(-45deg);
    transform-origin: center;
  }

  &::before {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    width: 29px;
    height: 4px;
    background: linear-gradient(238.08deg, #D4208C 0.42%, #E61726 82.5%);
    transform: translate(-50%, -50%);
    transform: translate(-50%, -50%) rotate(45deg);
    transform-origin: center;
  }
}

.ant-modal .ant-modal-close {
  &:hover {
    background-color: #ffffff;
  }
}
</style>
