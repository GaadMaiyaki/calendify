<template>
 
  <Header/>
  <section class="d-flex">
    <Calendar/>
  </section>

  <Footer/>
  
</template>


<script>

  import Calendar from './components/CalendarBody.vue';
  import Header from './components/AppHeader.vue'
  import Footer from './components/AppFooter.vue';


  export default {

    components:{
      Header,
      Calendar,
      Footer   
    }

}

</script>

<style>

</style>