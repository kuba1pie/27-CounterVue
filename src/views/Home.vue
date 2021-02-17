<template>
  <div class="Home">
    <h1>Time counter</h1>
    <p>Nowy licznik</p>
    <Form />
    <div class="Wrapper"></div>
    <Alert />
  </div>
</template>

<script>
import Form from "@/components/Form.vue";
import Alert from "@/components/Alert.vue";

export default {
  name: "Home",
  components: {
    Alert,
    Form
  }
};
</script>
