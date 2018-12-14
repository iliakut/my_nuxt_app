<template>
  <div>
    <label>{{ header }}</label>
    <input
      ref="datePicker"
      :value="date"
      type="text"
      class="form-control mr-sm-2, dark">
  </div>
</template>

<script>
import flatpickr from 'flatpickr'
import 'flatpickr/dist/themes/dark.css'

export default {
  name: 'DatePick',
  model: {
    prop: 'date'
  },
  props: {
    date: {
      type: [String],
      required: true
    },
    header: {
      type: String,
      required: true
    }
  },
  data: () => ({
    // экземпляр плагина
    fp: null
  }),
  watch: {
    // при измененити даты регистрации обновлять дату календаря
    date() {
      this.fp.setDate(this.date)
    }
  },
  //инициализация
  mounted() {
    this.init()
  },
  beforeDestroy() {
    this.fp.destroy()
  },
  methods: {
    init() {
      this.fp = flatpickr(this.$refs.datePicker, {
        // ицициализация отображения
        dateFormat: 'd.m.Y',
        // событие плагина
        onChange: (selectedDates, dateStr) => {
          // передает значение наверх
          this.$emit('input', dateStr)
        }
      })
    }
  }
}
</script>

<style scoped>
</style>
