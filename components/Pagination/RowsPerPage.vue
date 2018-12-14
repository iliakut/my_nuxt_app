<template>
  <div>
    <select @input="changed($event.target.value)">
      <option v-for="rows in rowsOnPage" :key="rows" :value="rows">
        {{ rows }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'RowsPerPage',
  data: () => ({
    rowsOnPage: [2, 5, 10, 100]
  }),
  methods: {
    changed(value) {
      this.$emit('changeRaws', value)
    }
  }
}
</script>
