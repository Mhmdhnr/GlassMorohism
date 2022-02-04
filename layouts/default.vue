<template>
  <nuxt />
</template>

<script>
    export default {
        name: "default",
        mounted() {
            this.$colorMode.preference = "light";
        }
    }
</script>

<style lang="scss" scoped>
  div {
    transition: background-color 500ms;
  }
</style>
