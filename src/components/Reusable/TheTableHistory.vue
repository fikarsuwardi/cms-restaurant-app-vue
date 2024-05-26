<script>
export default {
  name: "TheTableHistory",
  props: ["el"],
  methods: {
    changeFormatDate(date) {
      return new Date(date).toISOString().split("T")[0];
    },
  },
};
</script>

<template>
  <tr>
    <th scope="row">{{ el.id }}</th>
    <td>{{ el.name }}</td>
    <td>{{ el.description }}</td>
    <td>{{ el.updatedBy }}</td>
    <td>{{ changeFormatDate(el.createdAt) }}</td>
  </tr>
</template>
