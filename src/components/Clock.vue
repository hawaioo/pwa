<template>
  <div class="clock">
    <h1 class="clock__headline">Wecker</h1>
    <div class="clock__countdown">
      <span id="hh">{{ clockHours }}</span> :
      <span id="mm">{{ clockMinutes }}</span>
    </div>
    <div class="clock__icon-list">
      <button id="play" class="clock__icon">
        <PlayIcon v-if="!active" :size="iconSize" @click="activateClock" />
        <PauseIcon v-else :size="iconSize" @click="activateClock" />
      </button>
      <button id="settings" class="clock__icon">
        <SettingIcon :size="iconSize" @click="clockSetting" />
      </button>
      <button id="reset" class="timer__icon" @click="resetClock">
        <ResetIcon :size="iconSize" />
      </button>
    </div>

    <Modal ref="modal" title="Weckereinstellung">
      <div class="row">
        <div class="input-field col s6">
          <select id="hoursSelect" v-model="hoursSelected">
            <option
              v-for="hour in 24"
              :key="'hour' + hour"
              :selected="hour === 1"
              >{{ hour }}</option
            >
          </select>
          <label>Stunden</label>
        </div>

        <div class="input-field col s6">
          <select id="minutesSelect" v-model="minutesSelected">
            <option
              v-for="minute in 60"
              :key="'hour' + minute"
              :selected="minute === 1"
              >{{ minute }}</option
            >
          </select>
          <label>Minuten</label>
        </div>

        <div class="col s12" style="margin-top: 40px">
          <button @click="hideModal">Übernehmen</button>
        </div>
      </div>
    </Modal>
  </div>
</template>

<script>
import PlayIcon from "vue-material-design-icons/Play.vue";
import SettingIcon from "vue-material-design-icons/Cog.vue";
import PauseIcon from "vue-material-design-icons/PauseCircle.vue";
import ResetIcon from "vue-material-design-icons/LockReset.vue";
import Modal from "@/components/Modal";

export default {
  name: "Clock",
  components: {
    PlayIcon,
    SettingIcon,
    PauseIcon,
    ResetIcon,
    Modal
  },
  props: {
    minutes: {
      default: "00"
    },
    seconds: {
      default: "00"
    },
    hours: {
      default: "00"
    }
  },
  data() {
    return {
      iconSize: 30,
      hoursSelected: 0,
      minutesSelected: 0,
      paddingHour: 0,
      active: false
    };
  },
  computed: {
    clockMinutes() {
      return parseInt(this.minutes, 10) + parseInt(this.minutesSelected, 10);
    },
    clockHours() {
      const desiredHour =
        parseInt(this.hours, 10) + parseInt(this.hoursSelected, 10);
      if (this.clockMinutes >= 60) {
        this.clockMinutes - 60;
        desiredHour + 1;
      }
      if (desiredHour >= 24) {
        return desiredHour - 24;
      }
      return desiredHour;
    }
  },
  methods: {
    resetClock() {
      this.hoursSelected = 0;
      this.minutesSelected = 0;
    },
    hideModal() {
      this.$refs.modal.hide();
    },
    clockSetting() {
      this.$refs.modal.show();
    },
    activateClock() {
      this.active = !this.active;
    }
  }
};
</script>

<style lang="scss">
.clock {
  display: flex;
  justify-content: start;
  padding-left: 10%;
  flex-wrap: wrap;
  padding-bottom: 20px;

  @media (min-width: 400px) {
    justify-content: center;
  }

  &__icon-list {
    min-width: 300px;
  }
  &__headline {
    font-size: 16px;
    margin: 0;
    padding: 0;
  }
  &__countdown {
    width: 200px;
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
