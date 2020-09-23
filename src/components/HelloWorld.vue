<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="container">
      <form class="mt-5">
        <div class="form-group">
          <select
            id="currencychoice1"
            name="currencychoice1"
            class="form-control form-control-lg"
            v-model="currencychoice1"
          >
            <option v-for="c1 in currencychoice" :key="c1" required>{{ c1 }}</option>
          </select>
        </div>

        <div class="form-group">
          <select
            id="currencychoice2"
            name="currencychoice2"
            class="form-control form-control-lg"
            v-model="currencychoice2"
          >
            <option v-for="c2 in currencychoice" :key="c2" required>{{ c2 }}</option>
          </select>
        </div>

        <div class="form-group">
          <input type="date" v-model="date" class="form-control form-control-lg" id="date" />
        </div>

        <div class="form-group">
          <input
            type="number"
            v-model="number"
            class="form-control form-control-lg"
            id="number"
            min="1"
          />
        </div>

        <button type="submit" @click.prevent="process" class="btn btn-primary">Submit</button>
      </form>
      
      <div class="container" v-cloak v-show="displaydata">
        <h2 class="mt-5">To : {{ currencychoice1 }}</h2>
        <h2 class="mt-5">From : {{ currencychoice2 }}</h2>
        <h2 class="mt-5">Amount : {{ number }}</h2>
        <h2 class="mt-5">Conversion Rate : {{ conversionRate }}</h2>
        <h2 class="mt-5">Converted Amount : {{ amount }}</h2>
      </div>
      <div class="container" v-cloak v-show="displayerror">
        <h2 class="mt-5">We can't process your request.</h2>
      </div> 
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data: function() {
    return {
      displaydata: false,
      displayerror: false,
      currencychoice: [],
      currencychoice1: "USD",
      currencychoice2: "CAD",
      date: "2020-09-02",
      number: 1,
      conversionRate: 0,
      amount: 0
    };
  },
  created: function () {
      var urltofetchcurrency = "https://www.bankofcanada.ca/valet/groups/FX_RATES_DAILY";
      axios
        .get(urltofetchcurrency)
        .then(res => {
            console.log(res);
            //console.log(res.data.groupDetails.groupSeries[0].label);
            let f = res.data.groupDetails.groupSeries;
            for (var key in f){
              let temp = f[key]["label"].replace('/',' ').replace('CAD','');
              this.currencychoice.push(temp);
            }
            this.currencychoice.push("CAD");
            this.currencychoice.sort();
        })
        .catch(e => {
          console.log("Can't process your request." + e);
        });
  },
  methods: {
    process: function() {
      var apiKey = "FX" + this.currencychoice1 + this.currencychoice2;
      var url = "https://www.bankofcanada.ca/valet/observations/" + apiKey;
      axios
        .get(url)
        .then(res => {
          //console.log(res);
          //console.log(res.data);
          // console.log(typeof res.data.observations);
          let filteredData = res.data.observations.filter(
            f => f.d === this.date
          );
          if (filteredData.length > 0) {
            // console.log(filteredData[0][apiKey]);
            this.conversionRate = filteredData[0][apiKey]["v"];
            this.amount = (
              parseFloat(this.conversionRate) * this.number
            ).toFixed(4);
            this.displaydata = true;
            this.displayerror = false;
            // console.log(this.amount);
            // console.log(this.conversionRate);
          }
        })
        .catch(e => {
          this.displaydata = false;
          this.displayerror = true;
          console.log("Can't process your request." + e);
        });
    }
  }
};
</script>

<style>
[v-cloak] {
  display: none;
}
</style>