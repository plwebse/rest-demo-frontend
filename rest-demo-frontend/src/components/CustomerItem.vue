<script setup>
defineProps({
  name: {
    type: String,
  },
  address: {
    type: String,
  },
  email: {
    type: String,
  },
  telephone: {
    type: String,
  },
})
</script>


<template>
  <tr>
    <td>name</td>
    <td>{{ name }}</td>
    <td>address</td>
    <td>{{ address }}</td>
    <td>email</td>
    <td>{{ email }}</td>
    <td>telephone</td>
    <td>{{ telephone }}</td>
  </tr>
</template>


<style>
</style>
