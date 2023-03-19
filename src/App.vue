<!-- Use "Vue Language Features (Volar)" plugin for better experience -->

<!-- This is main route component (App.vue) -->
<!-- Template is a mandatory part -->
<template>
  <h1>{{ title }}</h1>
  <p>Welcome...</p>
  <br>

  <div v-show="inputFieldShow">
    <input type="text" ref="inputField" style="margin-right: 10px;">
    <button @click="handleClick">Click me!</button>
  </div>
  <br>

  <!-- v-show may be better option instead of v-if. This div needs to be injected in html file for faster operations.
  But when teleport used use v-if -->
  <teleport to="#popupModels" v-if="modalShow">
    <!-- using props. props must be declerated in Modal, otherwise we can't use them -->
    <!-- All props will be converted to string as default. Other formats need data binding -->
    <!-- <Modal header="Sign up Now" text="Get %50 discount!"/> -->

    <!-- header is an array below because of data binding (:) -->
    <!-- <Modal :header="['Sign up Now', 50]" text="Get %50 discount!"/> -->
    <!-- closeModal is a custom event which created by Modal component and being listened here -->
    <!-- <Modal :header="modalHeader" :text="modalText" theme="dark" @closeModal="toggleModal"/> -->

    <!-- Using "Slots". Passing template as slot to Modal component -->
    <Modal theme="sale" @closeModal="toggleModal">
      <!-- named slot template as "modalLinks" -->
      <template v-slot:modalLinks>
        <a href="#">Sign up Now!</a>
        <a href="#">More Info...</a>
      </template>

      <!-- these below will be injected between default <slot></slot> in the Modal component -->
      <h1>{{ this.modalHeader }}</h1>
      <p style="font-weight: bold;">{{ this.modalText }}</p>   
    </Modal>
  </teleport>

  <!-- these items below will be teleported to div named modals in the index.html -->
  <teleport to="#popupModels" v-if="modalTwoShow">
    <Modal theme="dark" @closeModal="toggleModalTwo">
      <h1>{{ this.modalTwoHeader }}</h1>
      <p style="font-weight: bold;">{{ this.modalTwoText }}</p>  

      <template v-slot:modalLinks>
        <a href="#">Sign up Now!</a>
      </template>
    </Modal>  
  </teleport>

  <button style="margin-right: 10px;" v-show="!modalShow" @click="toggleModal">Show Sign up</button>
  <button  v-show="!modalTwoShow" @click="toggleModalTwo">Show Newsletter</button>
</template>


<!--  These below are optional -->
<script>
import Modal from './components/Modal.vue'

export default {
  name: 'App',   
  components: {
    Modal
  },

  data() {
    return {
      title: "~ Vue Modal Project ~",
      inputFieldShow: false,
      // ------------------------
      modalShow: false,
      modalHeader: "TA2LSM Giweaway",
      modalText: "Sign up and get your free tools!",
      // ------------------------
      modalTwoShow: false,
      modalTwoHeader: "Sign up to the newsletter",
      modalTwoText: "For updates and promote codes!",      
    }
  },

  methods: {
    toggleModal() {
      this.modalShow = !this.modalShow;
    },
    toggleModalTwo() {
      this.modalTwoShow = !this.modalTwoShow;
    },

    handleClick() {
      // using "refs"
      // console.log(this.$refs.named);
      // console.log(this.$refs.name.value);

      // this.$refs.inputField.classList.add('active');
      this.$refs.inputField.focus();
      this.$refs.inputField.value = 'Enter some text here!';
    }
  },
}
</script>

<!-- These styles below will be injected in head section in html file -->
<style>
/* .popupModels class needs to be added when teleport is used or popupModels id can be used */
#app, #popupModels {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  border-bottom: 1px solid #ddd;
  display: inline-block;
  padding-bottom: 10px;
}
</style>
