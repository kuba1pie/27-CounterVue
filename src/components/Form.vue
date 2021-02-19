<template>
  <div class="Wrapper">
    <div class="Form">
      <b-form align="center">
        <label for="example-datepicker">Choose a date:</label>
        <b-form-datepicker
          id="example-datepicker"
          v-model="formDate"
          :start-weekday="1"
          hide-header
          class="mb-2"
        ></b-form-datepicker>
        <b-form-timepicker
          v-model="formHour"
          show-seconds
          :state="false"
          hide-header
          locale="de"
        ></b-form-timepicker>
      </b-form>

      <b-button class="addButton" variant="success" v-on:click="addCounter"
        >Add counter</b-button
      >
    </div>
    <div class="Dashboard">
      <div class="Counter" v-for="item in counters" :key="item.id">
        <div class="Watch" v-if="item.counter > now">
          <div class="Clock">
            <div class="Item">
              {{ Math.floor((item.counter - now) / 1000 / 3600 / 24) }}
            </div>
            <div class="Item">
              {{ Math.floor((item.counter - now) / 1000 / 3600) % 24 }}
            </div>
            <div class="Item">
              {{ Math.floor((item.counter - now) / 1000 / 60) % 60 }}
            </div>
            <div class="Item">
              {{ Math.floor((item.counter - now) / 1000) % 60 }}
            </div>
          </div>
          <b-button
            variant="danger outline-dark"
            v-on:click="deleteCounter(item.id)"
            >Delete Counter</b-button
          >
        </div>
        <div class="Alert" v-if="item.counter < now">
          <p>Countdown finished</p>
          <b-button
            variant="danger outline-dark"
            v-on:click="deleteCounter(item.id)"
            >Delete Counter</b-button
          >
          <b-button
            variant="info"
            v-on:click="resetCounter(item.diff)"
            v-b-popover.hover.top="
              'Due to assignment timer will be set to orginal intreval from now!'
            "
            title="Reset Counter!"
            >Reset Counter
          </b-button>
        </div>
      </div>
      <b-button variant="warning" v-on:click="clearCounter" class="clearButton"
        >Clear Local Storage</b-button
      >
    </div>
  </div>
</template>

<script>
export default {
  name: "Form",
  data() {
    return {
      formHour: "00:00:00",
      formDate: "2021-02-19",
      counters: [],
      local: "",
      now: "",
    };
  },
  methods: {
    addCounter() {
      let form = this.formDate + " " + this.formHour;
      this.counters.push({
        counter: new Date(new Date(form)),
        diff: this.now - new Date(form),
        id: this.counters.length + this.now,
      });
      this.local = JSON.stringify(this.counters);
    },
    resetCounter: function(message) {
      this.counters.push({
        counter: new Date(this.now.getTime() - message),
        diff: message,
        id: this.counters.length + this.now,
      });
      this.local = JSON.stringify(this.counters);
    },
    deleteCounter: function(message) {
      //alert(message);
      for (var i = 0; i < this.counters.length; i++) {
        if (this.counters[i].id === message) {
          this.counters.splice(i, 1);
          i--;
        }
      }
      this.local = JSON.stringify(this.counters);
    },
    clearCounter() {
      this.local = [];
      this.counters = [];
    },
    startTime() {
      setTimeout(this.startTime, 500);
      this.now = new Date();
    },
  },
  mounted() {
    if (localStorage.local) {
      this.local = localStorage.local;
      this.counters = JSON.parse(localStorage.local);
      for (var i = 0; i < this.counters.length; i++) {
        this.counters[i].counter = new Date(this.counters[i].counter);
      }
    }
    this.startTime();
  },
  watch: {
    local(newCounters) {
      localStorage.local = newCounters;
    },
  },
};
</script>
