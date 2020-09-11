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
              <!-- <div class="form-group">
                  <label for="email">Email</label>
                  <input type="email" v-model="email" id="email" class="form-control form-control-lg">
              </div> -->

              <!-- <div class="form-group">
                <input list="emails" name="emails" id="emails" class="form-control form-control-lg" v-model="email">
                  <datalist id="emailslist" >
                    <option v-for="e in email" :key="e">{{e}}</option>
                  </datalist>
              </div> -->


              <!-- <table class="table">
                <thead class="thead-light">
                    <th>Email</th>
                </thead>
                <tbody v-cloak>
                    <tr v-for="e in email" v-bind:key="e">
                      <td>{{e.text}}</td>
                    </tr>
                </tbody>
              </table> -->

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
      // email: [{ value: 1, text: "mike@example.com" },
      //        { value: 2, text: "kosha@gmail.com" }]
      // email: [{text: "mike@example.com"},{text: "kosha@gmail.com"}]
      currencychoice: ["USD", "EUR", "JPY", "GBP", "AUD", "CHF", "CNY", "HKD", "MXN", "INR"],
      currencychoice1: '',
      currencychoice2: '',
      date:''
      
    }
  }, 
  methods: {
    process: function () {
        alert("Submitted " + this.currencychoice1 + this.currencychoice2 + this.date);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<!-- <style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style> -->
<style scoped>
/* Dropdown Button */
.dropbtn {
  background-color: #4CAF50;
  color: white;
  padding: 16px;
  font-size: 16px;
  border: none;
}

/* The container <div> - needed to position the dropdown content */
.dropdown {
  position: relative;
  display: inline-block;
}

/* Dropdown Content (Hidden by Default) */
.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f1f1f1;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  z-index: 1;
}

/* Links inside the dropdown */
.dropdown-content a {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}

/* Change color of dropdown links on hover */
.dropdown-content a:hover {background-color: #ddd;}

/* Show the dropdown menu on hover */
.dropdown:hover .dropdown-content {display: block;}

/* Change the background color of the dropdown button when the dropdown content is shown */
.dropdown:hover .dropbtn {background-color: #3e8e41;}

[v-cloak] {
    display: none;
}
</style>
