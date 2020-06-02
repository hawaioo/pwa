<template>
  <div class="timer">
    <div id="placeholder" class="timer__wrapper">
      <p>Lokale Zeit</p>
      <div class="timer__countdown">
        <span id="hh">{{ hours }}</span> : <span id="mm">{{ minutes }}</span> :
        <span id="ss">{{ seconds }}</span>
      </div>

      <div v-for="(stopwatch, index) in stopwatches" :key="'stopwatch' + index">
        <Stopwatch></Stopwatch>
      </div>

      <div v-for="(clock, index) in clocks" :key="'clock' + index">
        <Clock :minutes="minutes" :seconds="seconds" :hours="hours"></Clock>
      </div>

      <div class="timer__controls">
        <button>
          <AddIcon
            class="timer__icon"
            :size="iconSize"
            @click="chooseAndAddClock"
          />
        </button>
      </div>
    </div>
    <portal to="globals">
      <Modal ref="modal" title="Weckertyp">
        <div class="timer__option-wrapper">
          <button class="timer__option" @click="newStopwatch">Stoppuhr</button>
          <button class="timer__option" @click="newClock">Wecker</button>
        </div>
      </Modal>
    </portal>
  </div>
</template>

<script>
import AddIcon from "vue-material-design-icons/BellPlus.vue";
import Modal from "@/components/Modal.vue";
import Stopwatch from "@/components/Stopwatch.vue";
import Clock from "@/components/Clock.vue";

export default {
  name: "Timer",
  components: {
    AddIcon,
    Modal,
    Stopwatch,
    Clock
  },
  data() {
    return {
      ticker: null,
      hours: null,
      minutes: null,
      seconds: null,
      iconSize: 45,
      stopwatches: [],
      clocks: []
    };
  },
  computed: {
    clockFormat() {
      return this.hours > 12 ? "pm" : "am";
    },
    date() {
      return new Date();
    }
  },
  methods: {
    // focusButton() {
    //   this.$refs.button.focus();
    // },
    chooseAndAddClock() {
      this.$refs.modal.show();
    },
    newStopwatch() {
      this.$refs.modal.hide();
      this.stopwatches.push("stopwatch");
    },
    newClock() {
      this.$refs.modal.hide();
      this.clocks.push("clock");
    },
    play() {},
    padZero(number) {
      if (number < 10) {
        return "0" + number;
      }
      return number;
    },
    getDate() {
      return new Date();
    },
    getMinutes() {
      return this.padZero(this.getDate().getMinutes());
    },
    getHours(twelveHour) {
      let hours = this.getDate().getHours();
      if (twelveHour && hours > 12) {
        hours = hours - 12;
      }
      return this.padZero(hours);
    },
    getSeconds() {
      return this.padZero(this.getDate().getSeconds());
    }
  },
  created() {
    this.ticker = setInterval(() => {
      this.minutes = this.getMinutes();
      this.hours = this.getHours(this.twelveHour);
      this.seconds = this.getSeconds();
    }, 1000);
  },
  destroyed() {
    clearInterval(this.ticker);
  }
};
</script>

<style lang="scss">
.timer {
  &__controls {
    position: relative;
    bottom: 0;
    display: flex;
    justify-content: center;
  }

  &__icon {
    cursor: pointer;
    padding: 0 20px;
  }

  &__wrapper {
    margin: auto;
    position: relative;
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
    margin: auto;
  }

  &__hours {
    padding-left: 3px;
    height: 45px;
    width: 80px;
    position: absolute;
  }
  &__minutes {
    padding-left: 80px;
    height: 45px;
    width: 80px;
    position: absolute;
  }
  &__seconds {
    padding-left: 160px;
    height: 45px;
    width: 80px;
    position: absolute;
  }

  &__option-wrapper {
    display: flex;
  }

  &__option {
    height: 200px;
    width: 50%;
  }
}
</style>
