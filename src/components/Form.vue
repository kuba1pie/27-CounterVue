<template>
  <div class="Form">
    <div>
      <b-form inline>
        <label for="example-datepicker">Choose a date</label>
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

      <b-button v-on:click="addCounter">Button</b-button>
      <b-button v-on:click="clearCounter">Clear Local Storage</b-button>
    </div>
    <li v-for="item in counters" :key="item.counter">
      <Counter
        v-bind:diff="item.counter - now"
        v-bind:difff="new Date(item.counter)"
        v-bind:date="item.counter"
        v-bind:now="now"
        v-bind:string="item.targetDate + ' ' + item.targetHour"
        :key="item.counter"
      />
      <b-button v-on:click="deleteCounter" :key="123">Delete Counter</b-button>
    </li>
  </div>
</template>

<script>
import Counter from "@/components/Counter.vue";

export default {
  name: "Form",
  components: {
    Counter,
  },
  data() {
    return {
      formHour: "08:00:00",
      formDate: "2021-03-01",
      counters: [],
      local: "",
      now: "",
    };
  },
  methods: {
    addCounter() {
      let formDate = Date.parse(this.formDate + " " + this.formHour);
      let formUtcDate = new Date(formDate);
      this.counters.push({
        counter: formUtcDate,
        targetDate: this.formDate,
        targetHour: this.formHour,
        // counter in utc
      });
      this.local = JSON.stringify(this.counters);
    },
    deleteCounter() {
      console.log("delete");
    },
    clearCounter() {
      this.local = [];
      this.counters = [];
    },
    startTime() {
      setTimeout(this.startTime, 500);
      this.now = new Date();
      //let nowUtc = ""
    },
    checkTime(i) {
      if (i < 10) {
        i = "0" + i;
      } // add zero in front of numbers < 10
      return i;
    },
  },
  mounted() {
    if (localStorage.local) {
      this.local = localStorage.local;
      this.counters = JSON.parse(localStorage.local);
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
