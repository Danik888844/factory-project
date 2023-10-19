<template>
  <div class="top-container">
      <h1 style="flex: 1; text-align: center;">Просмотр данных с cookie</h1>
      <button style="margin-right: 20px;" @click="toggleModal">Добавить фабрику</button>
  </div>
  <Content :factories="factories" />
  <div v-if="openModal">
    <Modal :cities="cities" :brigades="brigades" :shifts="shifts" :factories="factories" @close="toggleModal" />
  </div>
</template>

<script>
import Modal from './components/Modal.vue'
import Content from './components/Content.vue'
import VueCookies from "vue-cookie";

export default {
  name: 'App',
  components: {Modal, Content},
  data(){
    return{
      openModal: false,
      cities: [],
      brigades: [],
      shifts: [],
      factories: []
    }
  },
  created(){
    const savedData = VueCookies.get("savedData");

    if (savedData) {
      this.factories = JSON.parse(savedData);
    }
  },
  mounted(){
    fetch('http://localhost:3000/cities')
    .then((res)=>res.json())
    .then(data => this.cities = data)
    .catch(err => console.log(err.message))

    fetch('http://localhost:3000/brigades')
    .then((res)=>res.json())
    .then(data => this.brigades = data)
    .catch(err => console.log(err.message))

    fetch('http://localhost:3000/shifts')
    .then((res)=>res.json())
    .then(data => this.shifts = data)
    .catch(err => console.log(err.message))
  },
  methods: {
    toggleModal(){
      this.openModal = !this.openModal
    }
  }
}
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    background-color: white; 
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin-top: 40px;
    border-radius: 5px 5px 0 0;
  }
  .top-container{
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 2px solid whitesmoke;
  }
</style>
