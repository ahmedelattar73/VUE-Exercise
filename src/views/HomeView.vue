<template>
  <div class="home">
    <br>
    <img alt="Vue logo" src="../assets/logo.png">
    <HistoricalDataForm @submitted="getData"/>
    <HistoricalDataTable v-if="historicalData.length > 0" :historicalData="historicalData"/>
    <HistoricalChart v-if="historicalData.length > 0" :historicalData="historicalData"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HistoricalDataForm from '@/components/HistoricalDataForm.vue'
import HistoricalDataTable from "@/components/HistoricalDataTable";
import axios from "axios";
import HistoricalChart from "@/components/HistoricalChart";

export default {
  name: 'HomeView',
  components: {
    HistoricalChart,
    HistoricalDataTable,
    HistoricalDataForm
  },
  data() {
    return {
      historicalData: []
    }
  },
  methods: {
    getData(symbol, fromDate, toDate, email) {
      const config = {
        method: 'get',
        url: `http://localhost/api/historical-data?symbol=${symbol}&start_date=${fromDate}&end_date=${toDate}&email=${email}`,
        headers: {
          'Accept': 'application/json'
        }
      };

      let that = this
      axios(config)
          .then(function (response) {
            that.historicalData = response.data.data
          })
          .catch(function (error) {
            console.log(error);
          });
    }
  }
}
</script>
