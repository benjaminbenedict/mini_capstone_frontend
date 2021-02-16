<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>Now accepting Dogecoin</h2>
    <img
      src="https://static.independent.co.uk/2021/02/04/14/what%20is%20dogecoin.jpg?width=982&height=726&auto=webp&quality=75"
      alt=""
    />
  </div>
</template>

<style>
img {
  width: 250px;
  height: auto;
}
</style>

<script>
export default {
  data: function() {
    return {
      message: "Hot or Not Plant store!",
    };
  },
  created: function() {},
  methods: {},
};
</script>
