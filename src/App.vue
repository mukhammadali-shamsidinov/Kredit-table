<script >
import Form from './components/Form.vue';
import Table from './Table.vue';
import Calc from './components/Calc.vue';
export default {
  components:{
    Form,
    Table,Calc
  }
}
</script>

<template>
  <header>
   <div class="container mt-5">
    <div class="row">
  
        <Form />
        <Table />
        <!-- <Calc /> -->
    </div>
   </div>
  </header>

</template>

<style scoped>

</style>
