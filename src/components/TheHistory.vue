<script>
import TheTableHistory from './Reusable/TheTableHistory.vue'

export default {
  name: "TheHistory",
  components: {
    TheTableHistory
  },
  props: ["dataHistory"],
  emits: ["getDataHistory"],

  created() {
    this.$emit("getDataHistory")
  }
}
</script>

<template>
<!-- LIST HISTORY -->
    <section class="container-lg" id="history">
      <h1>HISTORY</h1>
      <table class="table table-striped" id="tableHistory">
        <thead>
          <tr>
            <th scope="col">Id</th>
            <th scope="col">Food Name</th>
            <th scope="col">Description</th>
            <th scope="col">By</th>
            <th scope="col">Created At</th>
          </tr>
        </thead>
        <tbody id="tableDataHistory">
          <TheTableHistory v-for="el in dataHistory" v-bind:el="el"/>
        </tbody>
      </table>
    </section>
    <!-- BATAS HISTORY -->
</template>