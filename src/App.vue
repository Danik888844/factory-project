<template>
  <div class="top-container">
      <h1 style="flex: 1; text-align: center;">Просмотр данных с cookie</h1>
      <button style="margin-right: 20px;" @click="toggleModal">Добавить фабрику</button>
  </div>
  <div v-if="openModal">
    <Modal @close="toggleModal" />
  </div>
</template>

<script>
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: {Modal},
  data(){
    return{
      openModal: false
    }
  },
  methods: {
    toggleModal(){
      this.openModal = !this.openModal
    }
  }
}
</script>

<style>
body{
  background-color: #ececec;
}
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    background-color: transparent; 
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin-top: 40px;
  }
  .top-container{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  button {
    width: auto;
    height: 30px;
    appearance: none;
    background-color: transparent;
    border: 2px solid #1A1A1A;
    border-radius: 5px;
    box-sizing: border-box;
    color: #3B3B3B;
    cursor: pointer;
    display: inline-block;
    font-size: 16px;
    font-weight: 600;
    line-height: normal;
    margin: 0;
    outline: none;
    text-align: center;
    text-decoration: none;
    transition: all 300ms cubic-bezier(.23, 1, 0.32, 1);
    user-select: none;
    -webkit-user-select: none;
    touch-action: manipulation;
    will-change: transform;
  }

button:disabled {
  pointer-events: none;
}

button:hover {
  color: #fff;
  background-color: #1A1A1A;
  box-shadow: rgba(0, 0, 0, 0.25) 0 8px 15px;
  transform: translateY(-2px);
}

button:active {
  box-shadow: none;
  transform: translateY(0);
}
</style>
