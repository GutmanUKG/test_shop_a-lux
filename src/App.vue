<template>
  <div id="app">
  <v-main-wrapper/>
  </div>
</template>

<script>
import VMainWrapper from "@/components/v-main-wrapper";
export default {
  name: 'app',
  components: {
    VMainWrapper

  }

}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
