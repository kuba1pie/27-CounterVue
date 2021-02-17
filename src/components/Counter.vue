<template>
  <div class="Counter">
    <div class="Hours">{{ diff.getHours() }}</div>
    <div class="Minutes">{{ diff.getMinutes() }}</div>
    <div class="Seconds">{{ diff.getSeconds() }}</div>
  </div>
</template>

<script>
export default {
  name: "Counter",
  props: ["date", "now", "diff"],
  data() {
    return {
      //data: new Date(this.date),
      //diff: new Date(this.date - this.now),
    };
  },
  mounted() {
    //this.diff = this.date - this.now;
  }
};
</script>
