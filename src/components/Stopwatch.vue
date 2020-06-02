<template>
  <div class="stop-watch" ref="abc">
    <h1 class="clock__headline">Stopuhr</h1>
    <div class="stop-watch__countdown">
      <span id="hh">{{ clockHours }}</span> :
      <span id="mm">{{ clockMinutes }}</span> :
      <span id="ss">{{ clockSeconds }}</span>
    </div>
    <div class="stop-watch__icon-list">
      <button id="play" class="timer__icon">
        <PlayIcon v-if="!active" :size="iconSize" @click="activateClock" />
        <PauseIcon v-else :size="iconSize" @click="activateClock" />
      </button>

      <button id="settings" class="timer__icon">
        <SettingIcon :size="iconSize" @click="clockSetting" />
      </button>
      <button id="reset" class="timer__icon" @click="resetClock">
        <ResetIcon :size="iconSize" />
      </button>

      <button class="timer__icon" @click="clockDelete">
        <DeleteIcon :size="iconSize"></DeleteIcon>
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
import ResetIcon from "vue-material-design-icons/LockReset.vue";
import PauseIcon from "vue-material-design-icons/PauseCircle.vue";
import DeleteIcon from "vue-material-design-icons/Delete.vue";
import Modal from "@/components/Modal";

export default {
  name: "Stopwatch",
  components: {
    PlayIcon,
    SettingIcon,
    ResetIcon,
    PauseIcon,
    DeleteIcon,
    Modal
  },
  data() {
    return {
      iconSize: 30,
      seconds: "00",
      minutes: "00",
      hours: "00",
      hoursSelected: 0,
      minutesSelected: 0,
      active: false,
      ticker: null
    };
  },
  computed: {
    clockMinutes() {
      return parseInt(this.minutesSelected, 10);
    },
    clockHours() {
      return parseInt(this.hoursSelected, 10);
    },
    clockSeconds() {
      return 0;
    },
    overallTime() {
      return (
        this.clockMinutes * 60 + this.clockHours * 60 * 60 + this.clockSeconds
      );
    }
  },
  methods: {
    resetClock() {
      this.minutesSelected = 0;
      this.hoursSelected = 0;
    },
    clockDelete() {
      this.$delete(this.$refs.abc);
    },
    clockSetting() {
      this.$refs.modal.show();
    },
    hideModal() {
      this.$refs.modal.hide();
    },
    activateClock() {
      this.active = !this.active;
      if (this.active) {
        this.activateTicker();
      } else {
        clearInterval(this.ticker);
      }
    },
    activateTicker() {
      const sanitizeHour = this.hoursSelected == 0 ? 1 : this.hoursSelected;
      const sanitizeMinute =
        this.minutesSelected == 0 ? 1 : this.minutesSelected;

      const deadline = new Date(
        Date.parse(new Date()) + sanitizeHour * sanitizeMinute * 60 * 1000
      );
      this.ticker = setInterval(() => {
        if (this.overallTime == 0) {
          clearInterval(this.ticker);
        }
        let time = Date.parse(deadline) - Date.parse(new Date());
        this.clockSeconds = Math.floor((time / 1000) % 60);
        this.clockMinutes = Math.floor((time / 1000 / 60) % 60);
        this.clockHours = Math.floor((time / (1000 * 60 * 60)) % 24);

        this.overallTime--;
      }, 1000);
    }
  }
};
</script>

<style lang="scss">
.stop-watch {
  display: flex;
  justify-content: start;
  padding-left: 10%;
  padding-bottom: 20px;
  flex-wrap: wrap;

  @media (min-width: 400px) {
    justify-content: center;
  }

  &__icon-list {
    min-width: 300px;
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
