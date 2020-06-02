<template>
  <div class="stop-watch">
    <div class="stop-watch__countdown">
      <span id="hh">{{ hours }}</span> : <span id="mm">{{ minutes }}</span> :
      <span id="ss">{{ seconds }}</span>
    </div>
    <button id="play" class="timer__icon">
      <PlayIcon :size="iconSize" />
    </button>

    <button id="settings" class="timer__icon">
      <SettingIcon :size="iconSize" />
    </button>
    <button id="reset" class="timer__icon">
      <ResetIcon :size="iconSize" />
    </button>
  </div>
</template>

<script>
import PlayIcon from "vue-material-design-icons/Play.vue";
import SettingIcon from "vue-material-design-icons/Cog.vue";
import ResetIcon from "vue-material-design-icons/LockReset.vue";

export default {
  name: "Stopwatch",
  components: {
    PlayIcon,
    SettingIcon,
    ResetIcon
  },
  data() {
    return {
      iconSize: 30,
      seconds: "00",
      minutes: "00",
      hours: "00"
    };
  }
};
</script>

<style lang="scss">
.stop-watch {
  display: flex;
  justify-content: center;
  &__countdown {
    width: 300px;
    height: 30px;
    top: 8px;
    left: 0;
    line-height: 28px;
    color: #becad8;
    font-size: 23px;
    text-align: center;
  }
}
</style>
