<template>
    <div>
      <table class="table table-bordered table-lightblue">
        <thead>
          <tr>
            <th>Month</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(month, index) in months" :key="index">
            <td>{{ month }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        startDate: '2024-01-05',
        endDate: '2024-12-14',
        months: [],
      };
    },
    mounted() {
      this.generateMonths();
    },
    methods: {
      generateMonths() {
        const start = new Date(this.startDate);
        const end = new Date(this.endDate);
  
        const monthsDiff = (end.getFullYear() - start.getFullYear()) * 12 + (end.getMonth() - start.getMonth());
        console.log(monthsDiff);
        const monthsArray = [];
        for (let i = 0; i <= monthsDiff; i++) {
          const currentDate = new Date(start.getFullYear(), start.getMonth() + i, 1);
          const monthName = currentDate.toLocaleString('default', { month: 'long' });
          monthsArray.push(monthName);
        }
  
        this.months = monthsArray;
      },
    },
  };
  </script>
  
  <style scoped>
  /* Add your custom styles here */
  .table-lightblue {
    background-color: lightblue;
  }
  </style>
  