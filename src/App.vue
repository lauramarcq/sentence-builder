<template>
  <TopNav></TopNav>
  <div class="min-h-full">
    <Header></Header>
    <main>
      <div class="mx-auto max-w-7xl py-6 sm:px-6 lg:px-8 min-h-screen">
        <MainStage></MainStage>
      </div>
    </main>
  </div>
</template>

<script>
import TopNav from "./components/TopNav.vue";
import Header from "./components/Header.vue";
import MainStage from "./components/MainStage.vue";

export default {
  name: "App",
  components: {
    TopNav,
    Header,
    MainStage,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
