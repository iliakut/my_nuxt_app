<template>
  <div>
    <p>Отображать пользователей на странице: {{ usersPerPage }}  </p>
    <rows-per-page
      @changeRaws="rows => usersPerPage = rows"
    />
  </div>
</template>

<script>
export default {
  name: 'Pagination',
  components: {
    'rows-per-page': () => import('@/components/Pagination/RowsPerPage')
  },
  data: () => ({
    usersPerPage: 2
  }),
  watch: {
    usersPerPage: function(val) {
      this.changed(val)
    }
  },
  methods: {
    changed(value) {
      this.$emit('changeRaws', value)
    }
  }
}
</script>
