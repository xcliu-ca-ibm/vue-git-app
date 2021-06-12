<template>
  <h2> Repos </h2>
  <ul v-for="repo in repos" :key="repo.id">
	  <li>{{ repo.full_name }}</li>
    <Issues :owner="repo.owner.login" :repo="repo.name" />
  </ul>
</template>

<script lang="ts">
  import GitRepo from "../types/Repo"
  import { defineComponent } from "vue"
  import { octokitClient } from "../composables/octokit"
  const octokit = octokitClient(localStorage.getItem("github-token") || "")
  import Issues from "./repo/Issues.vue"
  export default defineComponent({
    name: "Repos",
    components: { Issues },
    data() {
      return {
        repos: [] as GitRepo[]
      }
    },
    async created() {
      const { data: repos } = await octokit.request("/user/repos")
      this.repos = repos
    }
  })
</script>
