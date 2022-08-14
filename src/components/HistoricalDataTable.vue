<template>
  <div class="container">
    <div class="col-12">
      <h3>Historical data</h3>
    </div>
    <div class="table-wrapper">
      <div class="row">
        <div class="col-12">
          <table class="table table-dark mt-4">
            <thead>
            <tr>
              <td>Date</td>
              <td>Open</td>
              <td>High</td>
              <td>Low</td>
              <td>Close</td>
              <td>Volume</td>
            </tr>
            </thead>
            <tbody>
              <tr v-bind:key="index" v-for="(item, index) in historicalData">
                <td>{{ item.date }}</td>
                <td>{{ item.open }}</td>
                <td>{{ item.high }}</td>
                <td>{{ item.low }}</td>
                <td>{{ item.close }}</td>
                <td>{{ item.volume }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  name: "HistoricalDataTable",
  props: [
    'historicalData'
  ]
}
</script>

<style scoped>
  .table-wrapper {
    height: 500px;
    overflow-y: scroll;
  }
</style>