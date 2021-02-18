<template>
  <div class="Counter">
    <div class="Days">String in local time: {{ string }}</div>
    <div class="Days">
      Days:
      {{ Math.floor(dattt / 1000 / 60 / 60 / 24) }}
    </div>
    <div class="Days">
      Days:
      {{ Math.floor((date.getTime() - now.getTime()) / 1000 / 60 / 60 / 24) }}
    </div>
    <div class="Hours">
      Hour:
      {{ Math.floor(((date.getTime() - now.getTime()) / 1000 / 60 / 60) % 24) }}
    </div>
    <div class="Minutes">
      Min:
      {{ Math.floor(((date.getTime() - now.getTime()) / 1000 / 60) % 60) }}
    </div>
    <div class="Seconds">
      Sec:
      {{ Math.floor(((date.getTime() - now.getTime()) / 1000) % 60) }}
    </div>
  </div>
</template>

<script>
export default {
  name: "Counter",
  props: ["date", "diff", "now", "string", "difff"],
  data() {
    return { dattt: "" };
  },
  mounted() {
    this.dattt = this.now - this.difff;
    let jjj = new Date(this.date);
    this.utc = jjj.toUTCString();
    console.log(typeof this.diff);
    if (this.diff < 0) {
      console.log("<0");
    }
  },
};
</script>
