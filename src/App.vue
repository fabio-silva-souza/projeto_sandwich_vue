<template>
  <navbar :logo="logo_src" :alt="app_name"/>
  <router-view/>
  <Footer />
</template>

<script>
import Footer from './components/Footer.vue'
import Navbar from './components/Navbar.vue'

export default {
  components: { Navbar, Footer },
  data() {
    return {
      logo_src: "https://img.icons8.com/?size=512&id=QnlW7elBAFPH&format=png",
      app_name: "Faça seu lanche"
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@100;200;300;400;500;600;700;800;900&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Caprasimo&display=swap');
 
 *
 {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Poppins', sans-serif;
 }

  body
  {
    background-color: #1c1c1cf1;
    color: #fff;
  }

 .main-container
 {
  margin: 50px;
  min-height: 360px;
  
 }
 
 h1
 {
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #555;
 }
</style>
