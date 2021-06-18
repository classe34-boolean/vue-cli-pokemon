<template>
  <header>
      <h1>{{ title }}</h1>
  </header>
</template>

<script>
export default {
    name: "Header",
    props: {
        title: {
            type: String,
            default: function() {
                return "Titolo di default";
            }
        }
    }
}
</script>

<style>

</style>