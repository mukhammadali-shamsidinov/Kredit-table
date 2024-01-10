<script >
import Form from './components/Form.vue';
import Table from './Table.vue';
export default {
  components:{
    Form,
    Table
  }
}
</script>

<template>
  <header>
   <div class="container mt-5">
    <div class="row">
  
        <Form />
        <Table />
    </div>
   </div>
  </header>

</template>

<style scoped>

</style>
