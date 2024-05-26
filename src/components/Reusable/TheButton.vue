<script>
export default {
  name: "TheButton",
  emits: ["form"],
  methods: {
    submitFood() {
      this.$emit("form")
    }
  }
}
</script>

<template>
  <!-- REUSABLE BUTTON -->
  <button
    type="submit"
    class="btn btn-primary col-12"
    id="addButton"
    v-on:click.prevent="submitFood"
  >
    Submit
  </button>
</template>
