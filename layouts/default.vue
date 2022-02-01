<template>
  <nuxt />
</template>

<script>
    export default {
        name: "default",
        mounted() {
            let _this = this;
            let theme = "light";
            setInterval(function () {
                if (theme === "light") {
                    _this.$colorMode.preference = "dark";
                    theme = "dark";
                } else {
                    _this.$colorMode.preference = "light";
                    theme = "light";
                }
            }, 5000)
        }
    }
</script>

<style lang="scss" scoped>
</style>
