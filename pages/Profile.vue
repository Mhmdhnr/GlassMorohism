<template>
  <div>
    <ThemeToggle />
    <GlassBG :bgCount="5" :bgRangeMin="100" :bgRangeMax="150" :bgDurationRange="100000">
      <ProfileCard />
    </GlassBG>
  </div>
</template>

<script>
    import GlassBG from "../components/GlassBG";
    import ProfileCard from "../components/ProfileCard";
    import ThemeToggle from "../components/ThemeToggle";
    export default {
        name: "Profile",
        components: {ThemeToggle, ProfileCard, GlassBG}
    }
</script>

<style scoped>

</style>
