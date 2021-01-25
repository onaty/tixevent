<template>
  <div>
    <div v-if="isLoading">Is Check country for user</div>
    <div v-if="!isLoading">
      <!-- <h4>User Name:{{ countrydata.name }}</h4> -->
      <table class="table">
        <thead>
          <tr>
            <th>Country</th>
            <th>Probability</th>
            <th>Percentage</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="country in countrydata.country" :key="country.country_id">
            <td>{{ country.country_id }} </td>
            <td>{{ country.probability.toFixed('2')  }}</td>
            <td>{{ (country.probability * 100).toFixed('2') }}%</td>
          
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: () => {
    return {
      isLoading: true,
      countrydata: {},
    };
  },
  mounted() {
    axios
      .get(`https://api.nationalize.io/?name=${this.$route.params.name}`)
      .then((result) => {
        this.countrydata = result.data
        console.log(this.countrydata.name);
        this.isLoading = false;
      });
  },
  methods: {
  
  },
};
</script>