<script>
import TheForm from "./Reusable/TheForm.vue";

export default {
  name: "TheEditFood",
  components: {
    TheForm,
  },
  props: ["dataCategory", "dataDetailFood", "currentPage"],
  emits: ["submitFood"],
  methods: {
    editFood(objFood) {
      this.$emit("submitFood", objFood);
    },
  }
};
</script>

<template>
  <TheForm 
    v-bind:dataCategory="dataCategory" 
    v-on:submitFood="editFood"
    v-bind:dataDetailFood="dataDetailFood"
    v-bind:currentPage="currentPage"
  />
</template>
