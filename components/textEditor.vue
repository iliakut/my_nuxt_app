<template>

  <div>
    <label>О себе</label>
    <div>
      <vue-editor v-model="aboutUser"/>
    </div>
  </div>

</template>

<script>
import { VueEditor } from 'vue2-editor'
export default {
  name: 'TextEditor',
  components: {
    VueEditor
  },
  props: {
    about: {
      required: true,
      type: String
    }
  },
  data: function() {
    return {
      aboutUser: ''
    }
  },
  watch: {
    aboutUser: {
      deep: true,
      handler: function() {
        this.$emit('aboutUser', this.aboutUser)
      }
    }
  },
  created: function() {
    this.aboutUser = this.about
  }
}
</script>

<style scoped>
</style>
