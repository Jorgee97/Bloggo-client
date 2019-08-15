<template>
  <div class="w-full py-40 mx-auto max-w-xs">
    <form @submit="Login" class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="username">Username</label>
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          id="username"
          type="text"
          v-model="username"
          placeholder="Username"
        />
      </div>
      <div class="mb-6">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="password">Password</label>
        <input
          class="shadow appearance-none border border-red-500 rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
          id="password"
          type="password"
          v-model="password"
          placeholder="*******"
        />
        <p class="text-red-500 text-xs italic">{{output}}</p>
      </div>
      <div class="flex items-center justify-between">
        <button
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
          type="submit"
        >Sign In</button>
      </div>
    </form>
    <p class="text-center text-gray-500 text-xs">&copy;2019 Bloggo</p>
  </div>
</template>

<script>
export default {
  name: "Login",
  data() {
      return {
          username: '',
          password: '',
          output: ''
      };
  },
  methods: {
      Login(e) {
          e.preventDefault();
          let currentObj = this;
          this.axios.post('http://localhost:8080/login', {
              username: this.username,
              password: this.password,
              withCredentials: true,
              headers: { crossDomain: true, 'Content-Type': 'application/json' }
          })
          .then((response) => {
              console.log(response)
              if (response.status == 200) {
                  currentObj.output = ' ';
                  this.$router.push({path: '/dashboard'})
              }
          })
          .catch((err) => {
              currentObj.output = 'Username or password were not correct, please try again.'
          });
      }
  }
};
</script>