<script>
import TheTableFood from "./Reusable/TheTableFood.vue";

export default {
  name: "TheHome",
  components: {
    TheTableFood,
  },
  props: ["dataFood"],
  emits: ["getDataFood", "updateStatus", "goEditFood"],
  methods: {
    updateStatus(foodId, status) {
      this.$emit("updateStatus", foodId, status);
    },
    goEditFood(foodId) {
      this.$emit("goEditFood", foodId);
    },
  },
  created() {
    this.$emit("getDataFood");
  },
};
</script>

<template>
  <!-- LISTFOOD -->
  <section class="container-lg" id="listFood">
    <h1>FOOD LIST</h1>
    <table class="table table-striped table-bordered w-auto" id="tableListFood">
      <thead>
        <tr>
          <th scope="col">Id</th>
          <th scope="col">Name</th>
          <th scope="col">Description</th>
          <th scope="col">Price</th>
          <th scope="col" class="col-1">Status</th>
          <th scope="col">Image</th>
          <th scope="col">Author</th>
          <th scope="col">Category</th>
          <th scope="col">Action</th>
        </tr>
      </thead>
      <tbody id="tableDataFood">
        <TheTableFood
          v-for="el in dataFood"
          v-bind:el2="el"
          v-on:updateStatus="updateStatus"
          v-on:goEditFood="goEditFood"
        />
      </tbody>
    </table>
  </section>
  <!-- BATAS LISTFOOD -->
</template>
