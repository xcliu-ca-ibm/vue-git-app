<template>
  <h1> Github App </h1>
  <GithubTokenForm />
  <User />
  <Repos />
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import GithubTokenForm from "./components/GithubTokenForm.vue"
import User from "./components/User.vue"
import Repos from "./components/Repos.vue"

export default defineComponent({
  name: 'App',
  components: { GithubTokenForm, User, Repos },
})
</script>

<style>
#app {
  width: 400px;
  margin: auto;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
