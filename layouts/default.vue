<template>
  <nuxt />
</template>

<script>
    export default {
        name: "default",
        mounted() {
            let _this = this;
            setInterval(function () {
                _this.$colorMode.preference = "light";
            }, 5000)
        }
    }
</script>

<style lang="scss" scoped>
</style>
