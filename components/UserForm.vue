<template>
  <div>

    <div>
      <label>Имя</label>
      <!--      забиндим класс, если есть ошибка
      name - задается для vee-validate-->
      <input
        v-validate="'required'"
        v-model="userToChange.firstName"
        :class="{ 'is-invalid': errors.has('firstName') }"
        type="text"
        class="form-control mr-sm-2"
        name="firstName"
      >
      <span class="help-block text-danger">
        {{ errors.first('firstName') }}
      </span>
    </div>

    <div>
      <label>Фамилия</label>
      <input
        v-validate="'required'"
        v-model="userToChange.lastName"
        :class="{ 'is-invalid': errors.has('lastName') }"
        type="text"
        class="form-control mr-sm-2"
        name="lastName"
      >
      <span class="help-block text-danger">
        {{ errors.first('lastName') }}
      </span>
    </div>

    <date-pick
      v-model="userToChange.birthDate"
      :header="'Дата рождения'"
    />

    <!--
    отключить пререндернг
    -->
    <no-ssr>
      <avatar-Uploader
        v-model="userToChange.picture"/>
    </no-ssr>



    <div>
      <label>Баланс</label>
      <input
        v-model="userToChange.balance"
        type="text"
        class="form-control mr-sm-2"
      >
    </div>

    <div>
      <label>Email</label>
      <input
        v-validate="'required|email'"
        v-model="userToChange.email"
        :class="{ 'is-invalid': errors.has('email') }"
        type="text"
        class="form-control mr-sm-2"
        name="email"
      >
      <span class="help-block text-danger">
        {{ errors.first('email') }}
      </span>
    </div>

    <div>
      <label>Телефон</label>
      <input
        v-model="userToChange.phone"
        type="text"
        class="form-control mr-sm-2"
      >
    </div>

    <date-pick
      v-model="userToChange.registered"
      :header="'Зарегистрирован'"
    />

    <div>
      <label>Возраст</label>
      <input
        v-model="userToChange.age"
        type="text"
        class="form-control mr-sm-2"
      >
    </div>

    <div>
      <label>Компания</label>
      <input
        v-model="userToChange.company"
        type="text"
        class="form-control mr-sm-2"
      >
    </div>

    <text-editor
      :about="userToChange.about"
      @aboutUser="aboutUser => userToChange.about = aboutUser"
    />

    <pre>{{ userToChange }}</pre>
  </div>

</template>

<script>
export default {
  name: 'UserForm',
  //валидация для компонента выше
  inject: ['$validator'],
  components: {
    avatarUploader: () => import('@/components/AvatarUploader'),
    datePick: () => import('@/components/datePick'),
    textEditor: () => import('@/components/textEditor')
  },
  props: {
    user: {
      type: Object,
      required: true
    }
  },

  data: function() {
    return {
      userToChange: null,
      test: '123'
    }
  },

  watch: {
    userToChange: {
      deep: true,
      handler: function() {
        this.$emit('sendInput', this.userToChange)
      }
    }
  },

  created: function() {
    this.userToChange = Object.assign({}, this.user)
  }
}
</script>
<style>
span {
  width: 150px;
}
label {
  margin-top: 10px;
}
</style>
