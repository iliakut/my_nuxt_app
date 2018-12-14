<template>
  <div>
    <h2>Редактирование пользователя {{ id }}</h2>
    <div v-if="!user"
         class="alert alert-warning">
      Загрузка...
    </div>
    <user-form
      v-else
      :user="user"
      @sendInput="currUser => user = currUser"/>
    <button type="button" class="btn btn-dark" @click="save">Сохранить</button>
    <button type="button" class="btn btn-dark" @click="deleteUser">Удалить</button>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'EditUser',
  components: {
    'user-form': () => import('@/components/UserForm.vue')
  },
  data: function() {
    return {
      user: null
    }
  },
  computed: {
    id() {
      return this.$route.params.id
    },
    url() {
      return `http://localhost:3004/users/${this.id}`
    }
  },
  mounted() {
    this.loadUser()
  },
  methods: {
    loadUser() {
      axios
        .get(this.url)
        .then(response => response.data)
        .then(user => (this.user = user))
        .catch(error => console.log(error))
    },
    save() {
      // валидация
      this.$validator.validateAll()
      if (this.errors.any()) {
        alert('Заполнены не все поля')
        return
      }

      axios
        .patch(this.url, this.user)
        .then(() => {
          console.log('Данные отредатированы')
          this.$router.push({ path: '/users' })
        })
        .catch(error => console.log(error))
    },
    deleteUser() {
      axios
        .delete(this.url, this.user)
        .then(() => {
          console.log('Пользователь удален')
          this.$router.push({ path: '/users' })
        })
        .catch(error => console.log(error))
    }
  }
}
</script>

<style scoped>
button {
  margin: 3px;
}
</style>
