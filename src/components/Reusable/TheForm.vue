<script>
import TheButton from "./TheButton.vue";

export default {
  name: "TheForm",
  components: {
    TheButton,
  },
  props: ["dataCategory", "dataDetailFood", "currentPage"],
  emits: ["submitFood"],
  data() {
    return {};
  },
  computed: {
    objFood() {
      if (this.currentPage === "edit-food") {
        return {
          name: this.dataDetailFood.name,
          description: this.dataDetailFood.description,
          price: this.dataDetailFood.price,
          imgUrl: this.dataDetailFood.imgUrl,
          categoryId: this.dataDetailFood.categoryId,
        };
      } else {
        return {
          name: "",
          description: "",
          price: "",
          imgUrl: "",
          categoryId: "",
        };
      }
    },

    title () {
      if (this.currentPage === "edit-food") {
        return "EDIT FOOD"
      } else {
        return "ADD FOOD"
      }
    }
  },
  methods: {
    submitForm() {
      this.$emit("submitFood", this.objFood);
    },
  },
};
</script>

<template>
  <!-- REUSABLE FORM -->
  <section class="container-lg" id="add-edit-food">
    <h1>{{ title }}</h1>
    <form>
      <div class="form-group">
        <label>Food Name</label>
        <input
          type="text"
          class="form-control"
          id="name"
          placeholder="Enter Food Name"
          v-model="objFood.name"
        />
        <label>Description</label>
        <input
          type="text"
          class="form-control"
          id="description"
          placeholder="Enter Description"
          v-model="objFood.description"
        />
        <label>Price</label>
        <input
          type="number"
          class="form-control"
          id="price"
          placeholder="Enter Price"
          v-model="objFood.price"
        />
        <label>Image Url</label>
        <input
          type="text"
          class="form-control"
          id="imgUrl"
          placeholder="Enter Image Url"
          v-model="objFood.imgUrl"
        />
        <label>Category</label>
        <select
          id="categoryId"
          class="form-select form-select-md"
          aria-label=".form-select-sm example"
          v-model="objFood.categoryId"
        >
          <option v-for="el in dataCategory" v-bind:value="el.id">
            {{ el.name }}
          </option>
        </select>
      </div>
      <br />
      <TheButton v-on:form="submitForm" />
    </form>
  </section>
  <!-- BATAS REUSABLE FORM -->
</template>
