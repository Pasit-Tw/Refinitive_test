<template>
  <div class="container">
    <input
      v-model="filter"
      type="text"
      placeholder="Insert name of categories"
      class="my-2"
    />
    <table>
      <thead>
        <th>categories</th>
      </thead>
      <tr v-for="each in filters" v-bind:key="each">
        <td class="px-2 mx-2">
          {{ each }}
        </td>
      </tr>
    </table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      categories: [],
      filter: "",
    };
  },
  methods: {
    async getCategories() {
      const res = await fetch("https://api.publicapis.org/categories");
      const results = await res.json();
      this.categories = results;
    },
  },
  computed: {
    filters() {
      if (this.filter === "") {
        return this.categories;
      }
      return this.categories.filter((item) => {
        return item.toLowerCase().includes(this.filter.toLowerCase());
      });
    },
  },
  mounted() {
    this.getCategories();
  },
};
</script>
<style scoped>
table,
thead,
td,
input {
  border: 1px solid black;
}
</style>
