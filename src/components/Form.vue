<template>
    <div class="col-12">
       <form @submit.prevent="handleSubmit">
        <div class="row">
            <div class="col">
                <select name="" id="" class="form-select" required>
            <option value="moth">oylik</option>
            <option value="year">yillik</option>
        </select>
            </div>
            <div class="col">
                <input type="date" class='datepicker-here form-control' required>
            </div>
            <div class="col">
                <input type="date" class='datepicker-here form-control' required>
            </div>
            <div class="col">
                <select name="" id="" class="form-select" required>
            <option value="1">boshi</option>
            <option value="30">oxiri</option>
        </select>
            </div>
            <div class="col">
        <button class="btn btn-outline-dark w-50">Save</button>
       </div>
        </div>
     
      
       </form>
    </div>
</template>
<script>
import axios from 'axios'
export default {
    methods:{
        handleSubmit(e){
            function getMonthYearDateRange(start_date, end_date) {
  // Parse the input strings to create Date objects
  const startDate = new Date(start_date);
  const endDate = new Date(end_date);

  // Check if the input dates are valid
  if (isNaN(startDate) || isNaN(endDate)) {
    console.error('Invalid date format');
    return;
  }

  // Initialize an array to store the result
  const result = [];

  // Loop through the months between the start and end dates
  let currentDate = new Date(startDate);
  let i=0
  while (currentDate <= endDate) {
    const month = currentDate.toLocaleString('default', { month: '2-digit' });
    const day = currentDate.toLocaleString('default', { day: '2-digit' });
    const year = currentDate.getFullYear();
    i++
    // Add the formatted month and year to the result array
    result.push(
        {   id:i*12,
            funding_date:`${year}-${month}-${day}`,
            currency_type:null,
            currency_amount:null,
            num:null

        }
    );

    // Move to the next month
    currentDate.setMonth(currentDate.getMonth() + 1);
  }

  return result;
}

// Example usage:
const start_date = e.target[1].value;
const end_date = e.target[2].value;

const dateRange = getMonthYearDateRange(start_date, end_date);
axios.post('https://api.invest-portal.uz/api/v1/test-dynamic-table/data?token=9ec4a421-b15b-4897-99c1-ffb9dfd66431',dateRange).then(()=>{
    alert("success")
    window.location.reload()
}).catch(err=>{
    alert(err.message)
})
console.log(dateRange);


// axios.post('https://api.invest-portal.uz/api/v1/test-dynamic-table/data?token=9ec4a421-b15b-4897-99c1-ffb9dfd66431',
// x
// ).then(()=>{
//     console.log('nice');
// })
 
        }
    }
}
</script>
<style scoped>
    .datepicker{
	font-family: 'Exo 2', sans-serif;
}
.datepicker--cell.-range-to-{
	background: rgba(248, 206, 236, 0.4);
	border-color: rgba(248, 206, 236, 1);
}

.datepicker--cell.-selected-,.datepicker--cell.-selected-.-focus-{
	background-color: #f8ceec;
	color: #000000;
}
.datepicker--cell.-in-range-{
	background: rgba(248, 206, 236, 0.2);
}
.datepicker--cell-day {
    font-weight: 500;
    color: #000000;
}

</style>