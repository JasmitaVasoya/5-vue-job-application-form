<template>
  <div class="data-list">
    <UserDataList />
  </div>
</template>

<script>
import UserDataList from "@/components/user-data-list.vue";

export default {
  name: "HomeView",
  components: {
    UserDataList,
  },
};
</script>

<style scoped>
.data-list {
  margin-top: 20px;
}
</style>
