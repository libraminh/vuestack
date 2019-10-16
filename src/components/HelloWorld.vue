<template>
  <v-card>
    <v-card-title>
      <v-text-field
        v-model="search"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
    </v-card-title>

    <v-data-table 
      :headers="headers" 
      :items="posts" 
      :items-per-page="10" 
      class="elevation-1"
      :search="search"
      :loading="loading"
      loading-text="Loading... Please wait"
      >
    </v-data-table>
  </v-card>
</template>

<script>
/* eslint-disable */
export default {
  created() {
    this.fetchPosts();
  },
  data: () => ({
    search: '',
    loading: true,
    headers: [
      { text: "ID", value: "id", sortable: false, },
      { text: "UserId", value: "userId" },
      { text: "Title", value: "title" },
      { text: "Body", value: "body" },
    ],
    posts: [],
  }),
  methods: {
    async fetchPosts() {
      const postsRes = await fetch('https://jsonplaceholder.typicode.com/posts');
      const posts = await postsRes.json();
      this.posts = posts;
      this.loading = false;
    }
  },
};
</script>
