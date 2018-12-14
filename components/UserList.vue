<template>
  <div>

    <table class="table table-hover">
      <caption>
        Общее количество пользователей: {{ usersListLen }}
      </caption>
      <slot name="header">
        <thead>
          <tr>
            <th>#</th>
            <th>Имя</th>
            <th>Фамилия</th>
            <th>Активен</th>
            <th>Баланс</th>
            <th>Email</th>
            <th>Телефон</th>
            <th>Зарегистрирован</th>
          </tr>
        </thead>
      </slot>
      <tbody>
        <tr
          v-for="user in arrOfArrUsers[currentPage]"
          :key="user.id">
          <slot v-bind="user" name="row">
            <router-link :to="/edit/ + user.id">
              <td>{{ user.id }}</td>
            </router-link>
            <td>{{ user.firstName }}</td>
            <td>{{ user.lastName }}</td>
            <td>{{ user.isActive }}</td>
            <td>{{ user.balance }}</td>
            <td>{{ user.email }}</td>
            <td>{{ user.phone }}</td>
            <td>{{ user.registered }}</td>
          </slot>

        </tr>
      </tbody>

    </table>
    <div
      v-if="arrOfArrUsers.length > 1">
      <button v-for="(arr, index) in arrOfArrUsers"
              :key="index"
              class="btn btn-lg btn-primary"
              @click="changePage(index)"
      >{{ index + 1 }}</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'UserList',
  props: {
    // Список пользователей
    users: {
      type: Array,
      required: true
    },
    rows: {
      type: [String, Number],
      required: true
    }
  },
  data: () => ({
    shownTable: 'true',
    text: 'The text that is to be copied',
    currentPage: 0
  }),
  computed: {
    usersListLen: function() {
      return this.users.length
    },
    arrOfArrUsers: function() {
      return this.splitUsersToPages(this.rows, this.users)
    }
  },
  watch: {
    rows: function() {
      this.setCurrentPageToZero()
    }
  },
  methods: {
    splitUsersToPages(rows, users) {
      let arrOfArrUsers = []
      let currentUsersArray = []
      const listLen = users.length
      const numberOfArrays = Math.ceil(listLen / rows)

      for (let i = 0; i <= numberOfArrays - 1; i++) {
        let start = i * rows
        let end = rows - 1 + start
        currentUsersArray = users.slice(start, end + 1)
        arrOfArrUsers.push(currentUsersArray)
      }
      return arrOfArrUsers
    },
    changePage(buttonNum) {
      this.currentPage = buttonNum
    },
    setCurrentPageToZero() {
      this.currentPage = 0
    }
  }
}
</script>
<style scoped>
button {
  margin: 3px;
}
</style>
