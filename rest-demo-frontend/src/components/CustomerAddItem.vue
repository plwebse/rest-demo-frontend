<script setup lang="js">
import axios from 'axios';

</script>

<script lang="js">

const apiUrl = 'http://localhost:8080/customers';


  function addCustomer(event) {
    event.preventDefault();

    let data = {
      name: event.target.name.value,
      address: event.target.address.value,
      email: event.target.email.value,
      telephone: event.target.email.value,
    }


    console.log(data)

    axios.post(apiUrl, data)
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });

  }

</script>


<template>
  <form @submit="addCustomer">
    <label>name: <input type="text" name="name" /></label>
    <br />
    <label>address: <input type="text" name="address" /></label>
    <br />
    <label>email: <input type="text" name="email" /></label>
    <br />
    <label>telephone: <input type="text" name="telephone" /></label>
    <br />
    <input type="submit" value="Submit" />
  </form>
</template>


<style>
</style>
