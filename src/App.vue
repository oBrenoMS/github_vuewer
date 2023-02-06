<template>
  <v-app>
    <v-app-bar
      app
      color="pink"
    >
      <div class="d-flex align-center">
        <v-img
          alt="GitHub Logo"
          class="shrink mr-2"
          contain
          src="https://m.media-amazon.com/images/I/71VqUo6TkNL.png"
          transition="scale-transition"
          width="40"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/oBrenoMS/github_vuewer"
        target="_blank"
        text
      >
        <span class="mr-2">Meu GitHub</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
            <v-btn
        href="https://linkedin.com/"
        target="_blank"
        text
      >
        <span class="mr-2">Meu Linkedin</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <GithubVuewer/>
    </v-main>
  </v-app>
</template>

<script>
import GithubVuewer from './components/GithubVuewer';

export default {
  name: 'App',

  components: {
    GithubVuewer,
  },

  data: () => ({
    //
  }),
};
</script>
