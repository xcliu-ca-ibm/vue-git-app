<template>
  <h2>User</h2>
  <div>
    <img :src="userData.avatar_url" width="100" alt="avatar">
    <p>{{ userData.login }}</p>
  </div>
</template>

<script lang="ts">
  import GitUser from "../types/User";
  import { defineComponent } from "vue"
  import { octokitClient } from "../composables/octokit"
  const octokit = octokitClient(localStorage.getItem("github-token") || "")
  export default defineComponent({
    name: "User",
    data() {
      return {
        userData: {} as GitUser,
      };
    },
    async mounted() {
      const { data: userData } = await octokit.request("/user");
      this.userData = userData
    }
  })
</script>
