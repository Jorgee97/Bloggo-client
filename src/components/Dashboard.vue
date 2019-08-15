<template>
  <div class="flex">
    <div class="bg-indigo-700 h-screen w-16 shadow-2xl">
      <img class="h-14 w-14 mb-4 p-2" src="@/assets/images/home.png" alt="Home icon" />
      <img class="h-14 w-14 mb-4 p-2" src="@/assets/images/contract.png" alt="Create icon" />
      <img class="h-14 w-14 mb-4 p-2" src="@/assets/images/settings.png" alt="Settings icon" />
    </div>
    <div class="h-screen w-full">
      <div class="container mx-auto">
        <h1 class="text-5xl">Your Articles</h1>
        <div class="w-full border-indigo-400 border-2 h-auto rounded shadow-2xl py-6 px-6 mt-6" v-for="article in articles" v-bind:key="article.id">
            <h1 class="text-3xl font-bold">{{article.title.toUpperCase()}}</h1>
            <p class="text-xl">{{article.description}}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  mounted() {
    var currentObj = this;
    this.axios
      .get("http://localhost:8080/blog/dashboard")
      .then(response => {
        currentObj.articles = response.data;
      })
      .catch(err => {
        if (err.response) {
          if (err.response.status == 401) {
            this.$router.push({ path: "/" });
          }
        }
        console.error(err);
      });
  },
  props: ['articles'],
  name: "Dashboard",
  data() {
    return {
      articles: ""
    };
  },
  methods: {}
};
</script>