<template>
  <div id="app">
    <div class="container d-flex flex-column align-items-center justify-content-center">
      <h4 class="display-4 mb-5">COVID Data</h4>
      <PieChart :chartData="chartData" ></PieChart>

    </div>
  </div>
</template>

<script>
import axios from 'axios';
const apiKey = '8d0d3a74c978490aabcf2df398a15f7e';
import moment from 'moment';

import PieChart from './components/Pie';

export default {
  name: 'App',
  components: {
    PieChart
  },

  data() {
    return {
      chartData: {}
    }
  },

  async created() {
    try {
      const { data } = await axios.get(`https://api.covidactnow.org/v2/country/US.json?apiKey=${apiKey}`);
      const date = moment(data.lastUpdatedDate, 'YYYY-MM-DD').format('MMMM DD');

      const actuals = data.actuals;

      this.chartData = {
        cases: actuals.positiveTests,
        hospitals: actuals.hospitalBeds.currentUsageCovid,
        icus: actuals.icuBeds.currentUsageCovid,
        vaccinations: actuals.vaccinationsCompleted,
        deaths: actuals.deaths
      }


    } catch(e) {
      console.error(e);

    }
  }
}
</script>

<style>
 #app .container {
   height: 100vh;
 }
</style>
