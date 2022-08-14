<template>
  <div class="container">
    <div class="col-12">
      <h3>Filter Historical data</h3>
    </div>

      <form v-on:submit.prevent="submitted()">
        <div class="row">
            <div class="col-md-6">
              <input type="text" required v-model="symbol" class="form-control w-100 my-2">
            </div>
            <div class="col-md-6">
              <input type="email" required v-model="email" class="form-control w-100 my-2">
            </div>
            <div class="col-md-6">
              <input type="date" v-bind:class="isValid[1] ? '' : 'invalid border-danger' " required v-model="fromDate" class="form-control w-100 my-2">
              <div v-if="!isValid[1]" class="text-start text-danger">
                Please choose correct date.
              </div>
            </div>
            <div class="col-md-6">
              <input type="date"  v-bind:class="isValid[2] ? '' : 'invalid border-danger' " required v-model="toDate" class="form-control w-100 my-2">
              <div v-if="!isValid[2]" class="text-start text-danger">
                Please choose correct date.
              </div>
            </div>
          <div class="col-auto">
            <input type="submit" class="btn btn-primary">
          </div>
        </div>
      </form>
  </div>
</template>

<script>

export default {
  name: 'HistoricalDataForm',
  data() {
    return {
      symbol: 'AMRN',
      fromDate: new Date(),
      toDate: new Date(),
      email: 'sadsad@dvffvfd.com',
      isValid: [
          true,
          true,
          true,
          true
      ]
    }
  },
  methods: {
    submitted() {
      this.$emit('submitted', this.symbol, this.fromDate,this.toDate, this.email);
    }
  },
  watch: {
    fromDate() {
      if(this.fromDate > this.toDate || new Date(this.fromDate) > new Date()) {
          this.isValid[1] = false
      } else {
        this.isValid[1] = true
      }
    },
    toDate() {
      if(this.toDate < this.fromDate ||new Date(this.toDate) > new Date()) {
        this.isValid[2] = false
      } else {
        this.isValid[2] = true
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
