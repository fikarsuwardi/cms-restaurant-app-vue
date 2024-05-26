<script>
export default {
  name: "TheTableCategory",
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
    <td>{{ changeFormatDate(el.createdAt) }}</td>
    <td>{{ changeFormatDate(el.updatedAt) }}</td>
  </tr>
</template>
