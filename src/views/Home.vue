<template>
  <div>
    <Banner/>
    <div class="main__container">
    <h1>monte seu Burger</h1>
    <BurgerForm/>
    </div>
  </div>
</template>

<script>
import Banner from "../components/Banner.vue"
import BurgerForm from "../components/BurgerForm.vue"

export default {
  name : "Home",
  components: {
    Banner,
    BurgerForm
  }
  
}

</script>


