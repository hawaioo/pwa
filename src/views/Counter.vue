<template>
  <div class="counter">
    <Timer></Timer>
    <!-- <Weather></Weather> -->
  </div>
</template>

<script>
import Timer from "@/components/Timer.vue";
// import Weather from "@/components/Weather.vue";

export default {
  name: "Counter",
  components: {
    Timer
  },
  data() {
    return {};
  }
};
</script>
