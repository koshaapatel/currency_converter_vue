<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="container">
          <form class="mt-5">
            
              <div class="form-group">
                <select id="currencychoice1" name="currencychoice1" class="form-control form-control-lg" v-model="currencychoice1">
                  <option v-for="c1 in currencychoice" :key="c1" required>{{ c1 }}</option>
                </select>
              </div>

              <div class="form-group">
                <select id="currencychoice2" name="currencychoice2" class="form-control form-control-lg" v-model="currencychoice2">
                  <option v-for="c2 in currencychoice" :key="c2" required>{{ c2 }}</option>
                </select>
              </div>

              <div class="form-group">
                <input type="date" v-model="date" class="form-control form-control-lg" id="date" />
              </div>

              <div class="form-group">
                <input type="number" v-model="number" class="form-control form-control-lg" id="number" />
              </div>

              <button type="submit" @click.prevent="process" class="btn btn-primary">Submit</button>
          </form>
  </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data: function() {
    return {
      currencychoice: ["USD", "EUR", "JPY", "GBP", "AUD", "CHF", "CNY", "HKD", "MXN", "INR"],
      currencychoice1: '',
      currencychoice2: '',
      date:'',
      number: ''
      
    }
  }, 
  methods: {
    process: function () {
        alert("Submitted " + this.currencychoice1 +" " +this.currencychoice2+" " + this.date+" "+this.number);
    }
  }
};
</script>