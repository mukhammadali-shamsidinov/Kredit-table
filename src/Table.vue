<template>


<!-- modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h1 class="modal-title fs-5" id="exampleModalLabel">Modal title</h1>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <select name="" id="" class="form-select" v-on:change="selectBank" v-model="bank">
          <option v-for="data in tableBank" :key="data.id" :value="data.name" >{{ data.name }}</option>
        </select>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary" @click="addTableColumn" v-if="bank" data-bs-dismiss="modal">Save changes</button>
      </div>
    </div>
  </div>
</div>

<!-- /modal -->

    <div class="mt-5">
        <table class="table table-bordered table-striped table-primary table-lightblue">
      <thead>
        <tr>
          <th rowspan="2">No</th>
          <th rowspan="2">Date</th>
          <th colspan="2">Tashabbuskor</th>
          <th rowspan="2" :colspan="abroadBank.length" >Xorijiy investitsiya <i class="bi bi-bank" data-bs-toggle="modal" data-bs-target="#exampleModal"></i></th>
          <th rowspan="2">Davlat Kafolatidagi kredit <i class="bi bi-bank" data-bs-toggle="modal" data-bs-target="#exampleModal"></i></th>
          <th rowspan="2">Maxalliy Bank kredit <i class="bi bi-bank" data-bs-toggle="modal" data-bs-target="#exampleModal"></i></th>
          <th colspan="2">TJJ</th>
          <th colspan="2">Jami</th>
          <!-- Add more headers as needed -->
        </tr>

        <tr>
          
          <th colspan="1">Mill so'm</th>
          <th colspan="1">doll</th>
          <th v-for="x in abroadBank" :key="x">{{ x }}</th>
          <th colspan="1">Mill so'm</th>
          <th colspan="1">doll</th>
          <th colspan="1">Mill so'm</th>
          <th colspan="1">doll</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in tableData" :key="index">
          <td>{{ index + 1 }}</td>
          <td style="width: 200px;">{{ item.funding_date }}</td>
         <td>
          <input      @keypress="handleKeyDown(index, $event)" ref="inputs"  type="text" class="form-control" v-model="item.currency_type"  @input="updateValue(item.funding_date,index, $event.target.value,item.id)">
         </td>
         <td>
          <input @keypress="handleKeyDown(index, $event)" ref="inputs" type="text" class="form-control" v-model="item.currency_amount" @input="updateValue(item.funding_date,index, $event.target.value)">
         </td>
         <td>
          <input @keypress="handleKeyDown(index, $event)" ref="inputs" type="text" class="form-control" v-model="item.num" @input="updateValue(item.funding_date,index, $event.target.value)">
         </td>
         <td>
          <input @keypress="handleKeyDown(index, $event)" ref="inputs" type="text" class="form-control" v-model="item.num" @input="updateValue(item.funding_date,index, $event.target.value)">
         </td>
         <td>
          <input @keypress="handleKeyDown(index, $event)" ref="inputs" type="text" class="form-control" v-model="item.num" @input="updateValue(item.funding_date,index, $event.target.value)">
         </td>
         <td>
          <input @keydown="handleKeyDown(index, $event)" ref="inputs" type="text" class="form-control" v-model="item.num" @input="updateValue(item.funding_date,index, $event.target.value)">
         </td>
         <td>
          <input @keydown="handleKeyDown(index, $event)" ref="inputs" type="text" class="form-control" v-model="item.num" @input="updateValue(item.funding_date,index, $event.target.value)">
         </td>
         <td>
          <input type="text" class="form-control"  disabled :value="item.currency_type">
         </td>
         <td>
          <input type="text" class="form-control" disabled :value="item.currency_amount">
         </td>
         
      
          <!-- Add more columns as needed -->
        </tr>
      </tbody>
    </table>
    <button class="btn btn-info" @click="addSource">save</button>
    </div>
</template>
<script>
import axios from 'axios'
export default {
  data() {
    return {
      tableData: [],
      tableBank:[],
      bank:'',
      abroadBank:[],
      listCurrent:[],
      all:{
        allSom:0,
        allDoll:0
      },
    };

  },


  async mounted (){
 
   await axios.get('https://api.invest-portal.uz/api/v1/test-dynamic-table/data?token=9ec4a421-b15b-4897-99c1-ffb9dfd66431')
    .then(res=>{

        console.log(res.data.data);
        this.tableData = res.data.data
    }).catch(err=>{
      console.log(err);
    })

    axios.get('https://api.invest-portal.uz/api/v1/test-dynamic-table/sources?token=9ec4a421-b15b-4897-99c1-ffb9dfd66431')
    .then(res=>{
      console.log(res.data.data);
      this.tableBank = res.data.data
    })
  }
  ,
  methods:{
    updateValue(funding_date,index, key,id) {
      // Handle input changes and update the corresponding value in the data
      console.log(`Updating ${key} for person at index ${index}`);
     
     
    },
    handleKeyDown(index, event) {
      const inputs = this.$refs.inputs;

      switch (event.key) {
        case 'ArrowRight':
          if (index < inputs.length - 1) {
            // Saqlangan inputlardan biri ustiga o'tsa, keyingi inputni fokusga olish
            inputs[index + 1].focus();
          }
          break;
        case 'ArrowLeft':
          if (index > 0) {
            // Saqlangan inputlardan biri pastga o'tsa, oldingi inputni fokusga olish
            inputs[index - 1].focus();
          }
          break;
        case 'ArrowUp':
          // Yuqori inputa fokus qilish
          break;
        case 'ArrowDown':
          // Pastki inputa fokus qilish
          break;
        default:
          break;
      }
    },
    selectBank(){
      console.log(this.bank);
    },
    addTableColumn(){
      console.log(this.bank);
      this.abroadBank.push(this.bank)
      console.log(abroadBank);
    },
    addSource(){
      console.log(this.sourceAmount.xorij);
      
    },
    allSum(i){
      console.log(i);
    }
  }
};


</script>
<style scoped>
@import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css");
    .table-lightblue {
  background-color: lightblue;
  text-align: center;
}

table thead tr{
  vertical-align: middle;
}
input{
  border-radius: 0px !important;
}

td{
  min-width: 100px;
    position: relative;
}
td input{
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;   
}
</style>