<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
  </div>
</template>

<script>
// @ is an alias to /src
import PluginList from "@/components/PluginList.vue";

export default {
  name: "Home",
  components: {
    PluginList
  }
};
</script>
