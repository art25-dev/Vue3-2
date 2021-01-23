<template>
  <div class="container column">
    <form class="card card-w30">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select id="type" v-model="block">
          <option value="app-title">Заголовок</option>
          <option value="app-sub-title">Подзаголовок</option>
          <option value="app-avatar">Аватар</option>
          <option value="app-text">Текст</option>
        </select>
      </div>

      <div class="form-control">
        <label for="value">Значение</label>
        <textarea id="value" rows="3" v-model="textarea"></textarea>
      </div>

      <app-button :disabled="textarea.length < 4" @click.prevent="addBlock">Добавить</app-button>
    </form>

    <div class="card card-w70">

      <component v-for="item in blockList" :key="item.index" :is="item.name" :content="item.content">{{item.content}}</component>

      <h3 v-if="blockList.length === 0">Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
  </div>
  <div class="container">
    <p>
      <app-button @click="getComments" v-if="comments.length === 0"
        >Загрузить комментарии</app-button
      >
    </p>
    <div class="card" v-if="comments.length">
      <app-sub-title>Комментарии</app-sub-title>
      <ul class="list">
        <app-comment
          v-for="comment in comments"
          :key="comment.id"
          :mail="comment.email"
          >{{ comment.body }}</app-comment
        >
      </ul>
    </div>
    <app-loader v-if="loading"></app-loader>
  </div>
</template>

<script>
import AppButton from './components/AppButton'
import AppTitle from './components/AppTitle'
import AppSubTitle from './components/AppSubTitle'
import AppAvatar from './components/AppAvatar'
import AppText from './components/AppText.vue'
import AppComment from './components/AppComment'
import AppLoader from './components/AppLoader'

export default {
  data () {
    return {
      isActive: false,
      loading: false,
      comments: [],
      textarea: '',
      block: 'app-title',
      blockList: []
    }
  },
  methods: {
    async getComments () {
      this.loading = true
      const res = await fetch(
        'https://jsonplaceholder.typicode.com/comments?_limit=42',
        {
          method: 'GET'
        }
      )
      this.comments = await res.json()
      this.loading = false
    },
    addBlock () {
      const block = {
        name: this.block,
        content: this.textarea
      }

      this.blockList.push(block)
      this.textarea = ''
      this.block = 'app-title'
    }
  },
  computed: {},
  components: {
    AppButton,
    AppTitle,
    AppSubTitle,
    AppAvatar,
    AppText,
    AppComment,
    AppLoader
  }
}
</script>

<style></style>
