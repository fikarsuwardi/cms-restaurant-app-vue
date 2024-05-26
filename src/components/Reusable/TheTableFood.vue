<script>
export default {
  name: "TheTableFood",
  props: ["el2"],
  emits: ["updateStatus", "goEditFood"],
  data() {
    return {
      role: localStorage.getItem("role"),
      id: localStorage.getItem("id"),
    };
  },
  methods: {
    buttonUpdateStatus(foodId, status) {
      this.$emit("updateStatus", foodId, status);
    },
    buttonGoEditFood(foodId) {
      this.$emit("goEditFood", foodId);
    },
    formatRupiah(money) {
      return new Intl.NumberFormat("id-ID", {
        style: "currency",
        currency: "IDR",
        minimumFractionDigits: 0,
      }).format(money);
    },
    authz(id) {
      if(localStorage.role == 'admin') {
        return true
      } else if (localStorage.role == 'staff') {
        if (localStorage.id == id) {
          return true;
        } else {
          return false;
        }
      } else {
        return false
      }
    },
    statusLock() {
      if (localStorage.role == 'admin') {
        return true
      } else if (localStorage.role == 'staff') {
        return false
      }
    }
  },
};
</script>

<template>
  <tr>
    <th scope="row">{{ el2.id }}</th>
    <td>{{ el2.name }}</td>
    <td>{{ el2.description }}</td>
    <td>{{ formatRupiah(el2.price) }}</td>
    <td v-if="statusLock()">
      <select
        v-model="el2.status"
        v-on:change="buttonUpdateStatus(el2.id, el2.status)"
        
        id="status"
        class="form-select form-select-sm"
        aria-label=".form-select-sm example"
      >
        <option value="active">Active</option>
        <option value="inactive">Inactive</option>
        <option value="archived">Archived</option>
      </select>
    </td>
    <td v-else>{{ el2.status }}</td>
    <td>
      <img class="img-thumbnail" v-bind:src="el2.imgUrl" alt="" />
    </td>
    <td>{{ el2.User.username }}</td>
    <td>{{ el2.Category.name }}</td>
    <td>
      <button
        type="button"
        class="btn btn-primary"
        v-on:click.prevent="buttonGoEditFood(el2.id)"
        v-if="authz(el2.authorId)"
      >
        Edit
      </button>
    </td>
  </tr>
</template>
