<template>
  <div class="p-5 text-left font-raleway">
    <h1 class="font-bold text-left font-montserrat text-4xl sm:text-6xl mb-7">
      Sign Up
    </h1>
    <p v-show="error" class="text-sm text-red-500">{{ errorMsg }}</p>
    <form @submit="register">
      <div class="my-4">
        <h1 class="text-left font-bold mb-2 font-montserrat">Name</h1>
        <input
          type="text"
          v-model="name"
          class="
            text-sm
            outline-none
            pb-2
            w-4/5
            bg-transparent
            border-b
            hover:border-blue-700
            focus:border-blue-700
          "
        />
      </div>
      <div class="my-4">
        <h1 class="text-left font-bold mb-2 font-montserrat">Email</h1>
        <input
          type="email"
          v-model="email"
          class="
            text-sm
            outline-none
            pb-2
            w-4/5
            bg-transparent
            border-b
            hover:border-blue-700
            focus:border-blue-700
          "
        />
      </div>
      <div class="my-4">
        <h1 class="text-left font-bold mb-2 font-montserrat">Password</h1>
        <input
          type="password"
          v-model="password"
          class="
            text-sm
            outline-none
            pb-2
            w-4/5
            bg-transparent
            border-b
            hover:border-blue-700
            focus:border-blue-700
          "
        />
      </div>
      <div class="my-4">
        <h1 class="text-left font-bold mb-2 font-montserrat">Username</h1>
        <input
          type="text"
          v-model="username"
          class="
            text-sm
            outline-none
            pb-2
            w-4/5
            bg-transparent
            border-b
            hover:border-blue-700
            focus:border-blue-700
          "
        />
      </div>

      <button
        type="submit"
        :disabled="
          name.length < 2 || password.length < 6 || username.length < 3
        "
        class="bg-green-400 p-5 text-white"
      >
        Sign Up
      </button>
    </form>
  </div>
</template>
    <script>
import axios from "axios";

export default {
  name: "Register",
  data() {
    return {
      name: "",
      email: "",
      password: "",
      username: "",
      error: false,
      errorMsg: `An Error occurred, please try again`,
    };
  },
  methods: {
    async register(e) {
      try {
        e.preventDefault();
        await axios.post(`http://localhost:1337/api/auth/local/register`, {
          name: this.name,
          password: this.password,
          email: this.email,
          username: this.username,
        });
        this.$router.push("/");
      } catch (e) {
        this.error = true;
        this.email = "";
      }
    },
  },
};
</script>
    <style scoped>
</style>