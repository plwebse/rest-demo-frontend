<script setup lang="js">
import CustomerItem from './CustomerItem.vue'
import CustomerAddItem from './CustomerAddItem.vue'
</script>
<script lang="js">

import axios from 'axios';



export default {
  data() {
    return {
      page:0,
      totalNumberOfPages:0,
      hasNextPage:true,
      hasPreviousPage:true,
      itemsPerPage:20,
      allData: [],
      currentData: [],
    };
  },
  methods:{
    updatedPageInfo() {
        this.totalNumberOfPages = Math.max ((this.allData.length / this.itemsPerPage) -1, 0);
        console.log(this.totalNumberOfPages);

        this.hasNextPage = (this.totalNumberOfPages > 0 && this.page <= this.totalNumberOfPages) ? true : false;
        this.hasPreviousPage = (this.page > 0) ? true : false;

        console.log(this.page);
  },
    nextPage() {
      console.log("nextPage");

      this.page++;
      var start = this.page * this.itemsPerPage;
      var end = start + this.itemsPerPage;

      this.currentData =this.allData.slice(start, end);

      this.updatedPageInfo();

    },
    previousPage() {
      console.log("previousPage");
      this.page--;

      var start = this.page * this.itemsPerPage;
      var end = start + this.itemsPerPage;

      this.currentData =this.allData.slice(start, end);

      this.updatedPageInfo();

    },
  },

  mounted() {
    const apiUrl = 'http://localhost:8080/customers';

    axios.get(apiUrl)
      .then((response) => {
        this.allData = response.data;
        this.currentData = this.allData.slice(0, this.itemsPerPage);

        this.updatedPageInfo()
      })
      .catch((error) => {
        console.error('Error fetching data:', error);
      })
  },
}

</script>

<template>
  <table v-if="currentData">
    <CustomerItem
      v-for="item in currentData"
      :key="item.name"
      :name="item.name"
      :address="item.address"
      :email="item.email"
      :telephone="item.telephone"
    />
  </table>
  <p v-else>Loading...</p>

  <div v-if="hasNextPage"><button v-on:click="nextPage()">next page</button></div>
  <div v-if="hasPreviousPage"><button v-on:click="previousPage()">previous page</button></div>

  <div><customer-add-item /></div>
</template>


