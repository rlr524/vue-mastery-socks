<template>
  <div class="nav-bar"></div>
</template>

<script>
export default {
  name: "Header",
  data: function() {
    return {
      cart: 0,
    };
  },
};
</script>

<style>
.nav-bar {
  background: linear-gradient(-90deg, #84cf6a, #16c0b0);
  height: 60px;
  margin-bottom: 15px;
}
</style>
