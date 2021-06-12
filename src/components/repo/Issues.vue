<template>
  <div v-if="issues.length > 0">
    <h3> Issues </h3>
    <button @click="show_issues=!show_issues">{{ show_issues ? "Hide" : "Show" }}</button>
    <ul v-show="show_issues" v-for="issue in issues" :key="issue.id">
       <li><a :href="issue.url" target="_new">{{ issue.title }}</a></li>
    </ul>
  </div>
</template>

<script lang="ts">
  import GitIssue from "../../types/Issue"
  import { defineComponent } from "vue"
  import { octokitClient } from "../../composables/octokit"
  const octokit = octokitClient(localStorage.getItem("github-token") || "")
  export default defineComponent({
    name: "Issues",
    props: {
      owner: {
        type: String,
        required: true,
      },
      repo: {
        type: String,
        required: true,
      },
    },
    data() {
      return {
        issues: [] as GitIssue[],
        show_issues: false
      }
    },
    methods: {
      async getRepoIssues(owner="", repo="") {
        if (!owner || !repo) {
          return;
        }
        const { data: issues } = await octokit.issues.listForRepo({
          owner,
          repo,
        });
        this.issues = issues;
      },
    },
    watch: {
      repo: {
        immediate: true,
        handler(value) {
          this.getRepoIssues(this.owner, value)
        }
      },
      owner: {
        immediate: true,
        handler(value) {
          this.getRepoIssues(value, this.repo)
        }
      }
    }
  })
</script>
