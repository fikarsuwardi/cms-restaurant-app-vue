<script>
import TheTableCategory from './Reusable/TheTableCategory.vue'

export default {
  name: "TheCategory",
  components: {
    TheTableCategory
  },
  props: ["dataCategory"],
  emits: ["getDataCategory"],

  created() {
    this.$emit("getDataCategory")
  }
}
</script>

<template>
<!-- LIST CATEGORY -->
    <section class="container-lg" id="listCategory">
      <h1>CATEGORY LIST</h1>
      <table class="table table-striped">
        <thead>
          <tr>
            <th scope="col">Id</th>
            <th scope="col">Name</th>
            <th scope="col">Created At</th>
            <th scope="col">Updated At</th>
          </tr>
        </thead>
        <tbody id="tableDataCategory">
          <TheTableCategory v-for="el in dataCategory" v-bind:el="el"/>
        </tbody>
      </table>
    </section>
    <!-- BATAS LISCATEGORY -->
</template>