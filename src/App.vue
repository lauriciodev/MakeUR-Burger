<template>
 <div>
   <Navbar :logo="logo_src" :alt="appname" />
   <router-view/>
   <Footer/>
 </div>

</template>
<script>
 import Navbar from "./components/Navbar.vue"
  import Footer from "./components/Footer.vue"


export default{
  components: {
    Navbar,
    Footer
  },
  data(){
    return{
    logo_src: "/img/burger.png",
     alt:"make"
    }
  }
}


</script>
<style>

*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
body{
  overflow-x: hidden;
  background-color: aliceblue;
}

.main__container{
  margin: 50px;
  min-height: 250px;
}

h1{
  text-align: center;
  font-size: 3.5rem;
  color: rgb(255, 174, 0);
  margin: 50px 0;
}

</style>



