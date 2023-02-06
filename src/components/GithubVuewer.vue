<template>
  <v-container>
    <GithubRepo @reposelected="onRepoSelected"/>
    <GithubTree :repo="repo"/>
  </v-container>
</template>
  
<script>
  import GithubRepo from './GithubRepo';
  import GithubTree from './GithubTree';
  export default {
    components: {
      GithubRepo,
      GithubTree,
    },
    data: () => ({
      repo: null
    }),
    methods: {
      onRepoSelected(repo){
        this.repo = repo
      }
    }
  }
</script>
