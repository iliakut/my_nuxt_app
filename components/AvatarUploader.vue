<template>

  <div>
    <label>Аватарка</label>
    <input
      v-model="picture"
      type="text"
      class="form-control mr-sm-2" readonly>


    <input ref="image" type="file" class="hidden" readonly>

    <div>
      <img :src="picture">
    </div>
    <form>
      <vue-dropzone id="dropzone" ref="myVueDropzone" :options="dropzoneOptions"/>
    </form>
    <button type="button" class="btn btn-dark" @click="deleteAvatar()">
      Удалить
    </button>
    <!--
      загрузка фотографий с помощью кнопки
    <input ref="image" type="file" class="hidden" @change="upload()">
    <button type="button" class="btn btn-dark" @click="selectNewFile()">
      Выбрать новую...
    </button>
    //dropzone classic
    <form ref="dropzone" class="dropzone"/>
    -->
  </div>

</template>

<script>
//import axios from 'axios'
//import Dropzone from 'dropzone'
import vue2Dropzone from 'vue2-dropzone'
import 'vue2-dropzone/dist/vue2Dropzone.css'
import 'dropzone/dist/dropzone.css'

export default {
  name: 'AvatarUploader',
  components: {
    vueDropzone: vue2Dropzone
  },
  model: {
    prop: 'picture'
  },
  props: {
    picture: {
      type: String,
      required: true
    }
  },
  data: function() {
    return {
      // для Vue2 dropzone
      dropzoneOptions: {
        maxFiles: 1,
        url: 'https://api.imgur.com/3/image',
        paramName: 'image',
        acceptedFiles: 'image/*',
        headers: {
          'Cache-Control': null,
          'X-Requested-With': null,
          Authorization: 'Client-ID 2cc16b58de99649'
        },
        success: (file, response) => {
          this.setNewAvatar(response.data.link)
          this.$refs.image.value = ''
        }
      }
    }
  },
  /*  mounted() {
    //classic dropzone
    this.initDropzone()
  },*/
  methods: {
    /*//инициализация DropZone classic
    initDropzone() {
      new Dropzone(this.$refs.dropzone, {
        url: 'https://api.imgur.com/3/image',
        paramName: 'image',
        acceptedFiles: 'image/!*',
        method: 'post',
        maxFiles: 1,
        headers: {
          'Cache-Control': null,
          'X-Requested-With': null,
          Authorization: 'Client-ID 2cc16b58de99649'
        },
        success: (file, response) => {
          this.setNewAvatar(response.data.link);
          this.$refs.image.value = ''
        }
      })
    },*/
    // удалить аватар
    deleteAvatar() {
      this.setNewAvatar('')
      this.$refs.myVueDropzone.removeAllFiles(true)
    },
    //отправить наверх
    setNewAvatar(picture) {
      this.$emit('input', picture)
    }
    /*
      для загрузки фотографий с помощью кнопки
          selectNewFile: function() {
      this.$refs.image.click()
    },

    upload: function() {
      const url = 'https://api.imgur.com/3/image'
      const data = new FormData()
      data.append('image', this.$refs.image.files[0])

      const config = {
        headers: {
          Authorization: 'Client-ID 2cc16b58de99649'
        }
      }

      axios
        .post(url, data, config)
        .then(response => response.data)
        .then(response => {
          this.setNewAvatar(response.data.link)
          this.$refs.image.value = ''
        })
    }
    */
  }
}
</script>

<style scoped>
.hidden {
  display: none;
}
img {
  margin-top: 15px;
}
button {
  margin-bottom: 10px;
  width: 190px;
}
form {
  width: 190px;
  margin-top: 10px;
}
</style>
