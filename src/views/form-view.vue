<template>
  <div class="form">
    <ApplicationForm />
  </div>
</template>

<script>
import ApplicationForm from "@/components/application-form.vue";

export default {
  name: "HomeView",
  components: {
    ApplicationForm,
  },
};
</script>

<style scoped>
.form {
  margin-top: 20px;
}
</style>
