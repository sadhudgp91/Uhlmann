<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Uhlmann Group Test Web App Demo"/>

    <!-- DatePicker Area -->

    <div id="datepicker">
      <div>
      <label for="datepicker-placeholder">From Date:</label>
      <input name="fromDate" locale="en" type="date" v-model="dateFrom">
      </div>
      <span v-bind:style="{ 'border': 'none ' + chosenWidth + ' red' }">Selected Date: {{ dateFrom }}</span>

      <div>
      <label for="datepicker-placeholder">To Date:</label>
      <input name="dateTo" locale="en" type="date" v-model="dateTo">
      <br>
      <span v-bind:style="{ 'border': 'none ' + chosenWidth + ' red' }">Selected Date: {{ dateTo }}</span>
      </div>
      
      <br>
    </div>


    <!-- Dropdown Country Selection Area -->

    <div class="country-selection">
    <label for="country">Your Country: </label>
    <span>
      <select class="form-control" @change="changeCountryName($event)" v-model="selectedCountry">
      <option value="select" selectedCountry disabled>Select a Country Name below: </option>
      <option v-for="country in countries" :value="country" :key="country.value">{{ country.label }}</option>
      </select><br><br>
      <span v-bind:style="{ 'border': 'none ' + chosenWidth + ' red' }">Selected Country JSON Response: {{ selectedCountry }}</span>

    </span>
    </div>
    <br><br>

    <!-- Buttons Area -->

    <div id="buttonArea">
      <button v-on:click="showCountry">Accept</button>
      <button v-on:click="showQuit">Quit</button>
    </div>
    
</div>
</template>


<script>
import HelloWorld from './components/HelloWorld.vue'
import Vue from "vue";

//Country Selection List based on REST API / JSON FILE or ISO_Country Codes
//const JsonCountryList = require('countries.js'); can also be used
//The i18n-iso-countries is used for easy interoperability

import VueCountryCode from "vue-country-code-select";
const countries = require('i18n-iso-countries')
countries.registerLocale(require('i18n-iso-countries/langs/en.json'))

Vue.use(VueCountryCode);

export default {
  name: 'App',
  methods: {
      showCountry: function() {
          //this.selectedCountry = this.selectedCountry ? false: true;
          alert("You have selected the country: "+ this.selectedCountry.label + " from date:" + this.dateFrom + " to date:" + this.dateTo);
      }
  },
  computed: {
    countries () {
      const list = countries.getNames('en', { select: 'official' })
      return Object.keys(list).map((key) => ({ value: key, label: list[key] }))
    },
    chosenWidth() {
      return this.widthMappings[this.selectedCountry] || '1px'
    }
  },
  data() {
    return {
        //countryList: JsonCountryList,
        
        dateFrom:false,
        dateTo:false,
        selectedCountry: false,
        widthMappings: {
        Title: '8px',
        Category: '9px',
        },
        options: []
    };
  },
  components: {
    HelloWorld
  }
}
</script>



<!-- Styling Area -->


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
