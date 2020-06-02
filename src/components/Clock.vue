<template>
  <div class="clock">
    <h1 class="clock__headline">Wecker</h1>
    <div class="clock__countdown">
      <span id="hh">{{ clockHours }}</span> :
      <span id="mm">{{ clockMinutes }}</span>
    </div>
    <button id="play" class="clock__icon">
      <PlayIcon :size="iconSize" />
    </button>

    <button id="settings" class="clock__icon">
      <SettingIcon :size="iconSize" @click="clockSetting" />
    </button>
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
          <a
            id="backBtn"
            class="waves-effect waves-light btn pink accent-2"
            style="margin-bottom: 5px;"
          >
            <i class="large material-icons">arrow_back</i>
          </a>
          <a
            id="applyBtn"
            class="waves-effect waves-light btn pink accent-2"
            style="margin-bottom: 5px;"
            >Apply</a
          >
        </div>
      </div>
    </Modal>
  </div>
</template>

<script>
import PlayIcon from "vue-material-design-icons/Play.vue";
import SettingIcon from "vue-material-design-icons/Cog.vue";
import Modal from "@/components/Modal";

export default {
  name: "Clock",
  components: {
    PlayIcon,
    SettingIcon,
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
      paddingHour: 0
    };
  },
  computed: {
    clockMinutes() {
      // const desiredMinute = parseInt(this.minutes, 10) + this.minutesSelected;
      // if (desiredMinute > 60) {
      //   return desiredMinute - 60;
      // }
      console.log(this.minutes, this.minutesSelected);
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
    clockSetting() {
      this.$refs.modal.show();
    }
  }
};
</script>

<style lang="scss">
.clock {
  display: flex;
  justify-content: center;

  &__headline {
    font-size: 16px;
    margin: 0;
    padding: 0;
  }
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
