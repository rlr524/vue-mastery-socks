<template>
<div id="ProductDetails">
      <!-- use v-for to loop through the array -->
        <ul>
          <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
        </ul>

</div>
</template>

<script>
export default {
    name: "ProductDetails",
    props: {
        details: {
            type: Array,
            required: true
        }
    }
}
</script>

<style>

</style>