<template>
  <div id="settings-container" style="display:none">
    <h5>Reminder Interval</h5>
    <div class="row">
      <div class="input-field col s6">
        <select id="hoursSelect">
          <option value="0" selected>0</option>
        </select>
        <label>Hours</label>
      </div>

      <div class="input-field col s6">
        <select id="minutesSelect">
          <option value="0" selected>0</option>
        </select>
        <label>Minutes</label>
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
  </div>
</template>

<script>
export default {
  name: "Timer",
  data() {
    return {
      time: null
    };
  },
  methods: {
    newCounter() {
      setInterval(() => {}, 1000);
    }
    /*
    // Get totalAmount from localStorage and if there is positive value call timeSet() immediately
var totalAmount = localStorage.getItem('countDown') || 0,
    timeloop;

if (totalAmount) {
    timeSet()
}

function timeSet () {
    totalAmount--;
    // Refresh value in localStorage
    localStorage.setItem('countDown', totalAmount);

     // If countdown is over, then remove value from storage and clear timeout
     if (totalAmount < 0 ) {
         localStorage.removeItem('countDown');
         totalAmount = 0;
         clearTimeout(timeloop);
         return;
     }

    var minutes = parseInt(totalAmount/60);
    var seconds = parseInt(totalAmount%60);

    if(seconds < 10)
        seconds = "0"+seconds;

    $('#tminus').val(minutes + ":" + seconds);

    timeloop = setTimeout(timeSet, 1000);
}

$('.enterTime').click(function () {
    var reqVal = $('#request').val();
    var parAmt = parseInt(reqVal);

    if (timeloop) {
        clearTimeout(timeloop)
    }

    totalAmount = parAmt * 60;

    $('#request').val(" ");

    timeSet();
})

// Clear timeout and remove localStorage value when resetting form
$('#countdown').on('reset', function () {
    totalAmount = 0;
    clearTimeout(timeloop);
    localStorage.removeItem('countDown');
})
    */
  }
};
</script>

<style lang="scss">
.timer {
  &__wrapper {
    height: 50px;
    margin-left: auto;
    margin-right: auto;
    width: 300px;
    position: relative;
  }

  &__countdown {
    position: absolute;
    height: 30px;
    top: 8px;
    left: 0;
    line-height: 28px;
    color: #becad8;
    font-size: 23px;
    text-align: center;
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
}
</style>
