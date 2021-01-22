<template>
  <div class="container column">
    <form class="card card-w30">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select id="type">
          <option value="title">Заголовок</option>
          <option value="subtitle">Подзаголовок</option>
          <option value="avatar">Аватар</option>
          <option value="text">Текст</option>
        </select>
      </div>

      <div class="form-control">
        <label for="value">Значение</label>
        <textarea id="value" rows="3"></textarea>
      </div>

      <app-button>Добавить</app-button>
    </form>

    <div class="card card-w70">
      <app-title>Резюме Артема</app-title>
      <app-avatar
        link="https://cdn.dribbble.com/users/5592443/screenshots/14279501/drbl_pop_r_m_rick_4x.png"
      ></app-avatar>
      <app-sub-title>О себе</app-sub-title>
      <app-text text="123"></app-text>

      <h3>Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
  </div>
  <div class="container">
    <p>
      <app-button @click="getComments" v-if="!loading">Загрузить комментарии</app-button>
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
      loading: false,
      comments: []
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
      setTimeout(() => {
        this.loading = false
      }, 1000)
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
