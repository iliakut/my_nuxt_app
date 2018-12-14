<template>
  <div>
    <header>
      <nav class="navbar navbar-expand-md navbar-dark fixed-top bg-dark">
        <div class="collapse navbar-collapse">
          <ul class="navbar-nav mr-auto">
            <nuxt-link tag="li"
                       to="/"
                       class="nav-link"
                       exact>
              <a class="nav-link"
                 href="#">Главная</a>
            </nuxt-link>

            <nuxt-link tag="li"
                       to="/Users"
                       class="nav-link" exact>
              <a class="nav-link"
                 href="#">Список пользователей</a>
            </nuxt-link>

            <nuxt-link tag="li"
                       to="/Add"
                       class="nav-link"
                       exact>
              <a class="nav-link"
                 href="#">Добавить пользователя</a>
            </nuxt-link>
          </ul>
        </div>
      </nav>
    </header>
    <main
      role="main"
      class="container">

      <nuxt/>

    </main>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  margin-top: 60px;
}
main {
  margin-top: 100px;
}
</style>
