<template>
  <div>
    <div>
      This is my Nuxt App.
    </div>
    <div>
      If you run fake server you can see users's list.
      <nuxt-link to="/Users"
                 class="nav-link" exact>
        <a class="nav-link"
           href="#">Список пользователей</a>
      </nuxt-link>
    </div>
    <div>
      If don't, you can try Add user page. It has First, Second Name validation, Email Validation, DropZone plugin to drag and drop your images to Imgur
      <nuxt-link tag="li"
                 to="/Add"
                 class="nav-link"
                 exact>
        <a class="nav-link"
           href="#">Добавить пользователя</a>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home'
}
</script>
