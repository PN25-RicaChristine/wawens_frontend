<template>
  <div id="app">
    <navigationbar></navigationbar>
      <router-view></router-view>
    <!-- <footerbar></footerbar> -->
  </div>
</template>
<script>
import navigationbar from "@/components/frame/Header.vue";
// import footerbar from "@/components/Footer.vue";

export default {
  name: "App",

  components: {
    navigationbar,
    // footerbar
  },

  data: () => ({})
};
</script>
<style>
#app{
  /* background-image: url('~@/assets/wallpaper.png'); */
  /* margin-top: 4.8%; */
  /* background-size:cover;
  background-repeat: no-repeat; */
}
</style>



