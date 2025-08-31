<script setup lang="js">
import CustomerItem from './CustomerItem.vue'
import CustomerAddItem from './CustomerAddItem.vue'
</script>

<template>
  <table v-if="apiData">
    <CustomerItem
      v-for="item in apiData"
      :key="item.name"
      :name="item.name"
      :address="item.address"
      :email="item.email"
      :telephone="item.telephone"
    />
  </table>
  <p v-else>Loading...</p>

  <div><customer-add-item /></div>
</template>

<script lang="js">

import axios from 'axios';

export default {
  data() {
    return {
      apiData: null,
    };
  },

  mounted() {
    const apiUrl = 'http://localhost:8080/customers';

    axios.get(apiUrl)
      .then((response) => {
        this.apiData = response.data;
      })
      .catch((error) => {
        console.error('Error fetching data:', error);
      });
  },
};




</script>
