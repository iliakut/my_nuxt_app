<template>
  <div class="about">
    <h1>Список пользователей</h1>
    <pagination-form
      @changeRaws="usersPerPage => rows = usersPerPage"
    />
    <div
      v-if="!users.length"
      class="alert alert-warning">
      Загрузка...
    </div>
    <user-list
      v-else
      :users="users"
      :rows="rows">
      <!--слот заголовка-->
      <thead slot="header">
        <tr>
          <th>#</th>
          <th>Имя</th>
          <th>Фамилия</th>
          <th>Email</th>
          <th>Телефон</th>
        </tr>
      </thead>
      <!--
      слот для таблицы пользователей
      slot-scope - для указания имени переменной,
      которая привязана в нутри копонента
      -->
      <template slot="row" slot-scope="user">
        <nuxt-link :to="'/users/edit/?id=' + user.id">
          <td>{{ user.id }}</td>
        </nuxt-link>
        <td>{{ user.firstName }}</td>
        <td>{{ user.lastName }}</td>
        <td>{{ user.email }}</td>
        <td>{{ user.phone }}</td>
      </template>
    </user-list>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Users',
  components: {
    'user-list': () => import('@/components/UserList.vue'),
    'pagination-form': () => import('@/components/Pagination/Pagination.vue')
  },
  data: () => ({
    users: [],
    rows: '2'
  }),
  computed: {},
  mounted() {
    this.loadUsers()
  },
  methods: {
    loadUsers() {
      axios
        .get('http://localhost:3004/users')
        .then(response => response.data)
        .then(users => (this.users = users))
        .catch(error => console.log(error))
    }
  }
}
</script>

<style scoped>
h1 {
  color: #2e041e;
}
</style>
