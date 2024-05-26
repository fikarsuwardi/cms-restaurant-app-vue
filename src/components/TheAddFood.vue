<script>
import TheForm from "./Reusable/TheForm.vue";

export default {
  name: "TheAddFood",
  components: {
    TheForm,
  },
  props: ["dataCategory"],
  emits: ["submitFood"],
  methods: {
    addNewFood(objFood) {
      this.$emit("submitFood", objFood);
    },
  }
};
</script>

<template>
  <TheForm 
    v-bind:dataCategory="dataCategory" 
    v-on:submitFood="addNewFood"
  />
</template>
