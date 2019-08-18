<template>
  <div class="flex h-screen">
    <div class="bg-indigo-700 h-screen w-16 shadow-2xl">
      <img class="h-14 w-14 mb-4 p-2" src="@/assets/images/home.png" alt="Home icon" />
      <img class="h-14 w-14 mb-4 p-2" src="@/assets/images/contract.png" alt="Create icon" />
      <img class="h-14 w-14 mb-4 p-2" src="@/assets/images/settings.png" alt="Settings icon" />
    </div>
    <div class="container mx-auto w-screen flex">
      <form class="rounded shadow-2xl h-auto w-full m-5 px-5 py-5">
        <label class="block text-black text-lg font-bold mb-2" for="title">Title</label>
        <input
          id="title"
          v-model="title"
          class="shadow mb-2 appearance-none border-2 border-indigo-700 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
        />
        <label class="block text-black text-lg font-bold mb-2" for="description">Description</label>
        <input
          id="description"
          v-model="description"
          class="mb-2 shadow appearance-none border-2 border-indigo-700 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
        />
        <label class="block text-black text-lg font-bold mb-2" for="content">Content 
            <button class="text-sm" @click="toHTML">Preview</button></label>
        <textarea
          id="content"
          rows="19"
          class="py-1 px-1 markdown resize-none shadow appearance-none rounded w-full border-indigo-700 border-2"
          v-model="markdown"      
        />
      </form>
      <div class="markdown" v-html="renderedMarkdown">{{ renderedMarkdown }}</div>
    </div>
  </div>
</template>

<script>
import MarkdownIt from "markdown-it/dist/markdown-it";

export default {
  name: "Creator",
  data() {
    return {
      markdown: "",
      renderedMarkdown: "",
      title: "",
      description: ""
    };
  },
  methods: {
    toHTML() {
      var md = MarkdownIt();
      var result = md.render(this.markdown);

      this.renderedMarkdown = result;
    }
  }
};
</script>