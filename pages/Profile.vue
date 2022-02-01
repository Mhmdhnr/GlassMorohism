<template>
  <GlassBG :bgCount="20" :bgRangeMin="70" :bgRangeMax="100" :bgDurationRange="50000">
    <ProfileCard />
  </GlassBG>
</template>

<script>
    import GlassBG from "../components/GlassBG";
    import ProfileCard from "../components/ProfileCard";
    export default {
        name: "Profile",
        components: {ProfileCard, GlassBG}
    }
</script>

<style scoped>

</style>
