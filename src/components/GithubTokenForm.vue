<template>
  <h2>Identity</h2>
  <form @submit.prevent="saveToken">
    <label> github token: 
      <input type="password" v-model="token">
    </label>
    <button type="submit">submit</button>
  </form>
</template>

<script lang="ts">
  import { defineComponent } from "vue"
  export default defineComponent({
	  name: "GithubTokenForm",
	  data() {
		  return {
		    token: localStorage.getItem("github-token") || ""
		  }
	  },
	  methods: {
		  saveToken() {
			  localStorage.setItem("github-token", this.token)
		  }
	  }
  })
</script>