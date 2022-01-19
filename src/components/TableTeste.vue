<template>
  <div>
    <v-data-table
      :headers="headers"
      :items="items"
      :options.sync="options"
      :server-items-length="itemsLength"
      :loading="loading"
      :itemsPerPage=5
      :footer-props="{ itemsPerPageOptions: [5, 10, 15, 20, itemsLength]}"
      class="elevation-1"
    >
    </v-data-table>
  </div>
</template>

<script>

export default {
  props: {
    headers: {
      type: Array,
    },
    items: {
      type: Array,
    },
    options: {
      type: Object,
    },
    itemsLength: {
      type: Number,
    },
    loading: {
      type: Boolean,
    },
  },
  computed: {
    changed() {
      return this.$emit('update:options', this.options);
    },
  },
};
</script>
