<template>
  <!-- <ul class="grid grid-cols-3 gap-3 px-5 py-24 mx-auto justify-items-center">
    <li v-for="post of posts.data" :key="post.id">
      <div class="max-w-sm rounded overflow-hidden shadow-lg">
        <img :src="image + post.attributes.course_img.data.attributes.url" />
        <div class="px-6 py-4">
          <div class="font-bold text-xl mb-2">
            {{ post.attributes.course_name }}
          </div>
          <p class="text-gray-700 text-base">
            {{ post.attributes.course_desc }}
          </p>
        </div>
      </div>
    </li>
  </ul> -->
  <div>
    <ul
      class="
        lg:flex lg:flex-row lg:justify-center
        flex flex-col
        justify-center
        items-center
      "
      id="category-section"
    >
      <button
        class="
          text-gray-900
          bg-gradient-to-r
          from-teal-200
          to-lime-200
          hover:bg-gradient-to-l hover:from-teal-200 hover:to-lime-200
          focus:ring-4 focus:ring-lime-200
          dark:focus:ring-teal-700
          font-medium
          rounded-lg
          text-sm
          px-5
          py-4
          text-center
          mr-2
          mb-2
        "
        @click="showPost('all')"
      >
        ALL
      </button>
      <li v-for="category of categories.data" :key="category.id">
        <button
          class="
            text-white
            bg-gradient-to-br
            from-pink-500
            to-orange-400
            hover:bg-gradient-to-bl
            focus:ring-4 focus:ring-pink-200
            dark:focus:ring-pink-800
            font-medium
            rounded-lg
            text-sm
            px-5
            py-4
            text-center
            mr-2
            mb-2
          "
          @click="showPost(category.attributes.category_name)"
        >
          {{ category.attributes.category_name }}
        </button>
      </li>
    </ul>
  </div>
  <ul class="flex flex-wrap justify-center mt-0 -m-4 py-4" id="cards-section">
    <li
      v-for="post of posts.data"
      :key="post.id"
      class="p-20 md:w-1/3 card-container"
    >
      <div
        class="
          h-full
          border-2 border-gray-200 border-opacity-60
          rounded-lg
          overflow-hidden
          shadow-2xl
          image-card
          perspective-left
        "
      >
        <router-link :to="{ name: 'details', params: { id: post.id } }">
          <img :src="image + post.attributes.course_img.data.attributes.url"
        /></router-link>
        <div class="p-6">
          <h2
            class="
              tracking-widest
              text-s
              title-font
              font-medium
              text-red-500
              mb-1
            "
          >
            {{ post.attributes.course_price }}$
          </h2>
          <h1 class="title-font text-lg font-medium text-gray-900 mb-3">
            {{ post.attributes.course_name }}
          </h1>
          <p class="leading-relaxed mb-3">
            {{ post.attributes.course_desc }}
          </p>
          <div class="flex items-center flex-wrap">
            <router-link :to="{ name: 'details', params: { id: post.id } }">
              <a
                class="text-indigo-500 inline-flex items-center md:mb-2 lg:mb-0"
                >Learn More
                <svg
                  class="w-4 h-4 ml-2"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                  stroke-width="2"
                  fill="none"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <path d="M5 12h14"></path>
                  <path d="M12 5l7 7-7 7"></path>
                </svg> </a
            ></router-link>

            <span
              class="
                text-gray-400
                mr-3
                inline-flex
                items-center
                lg:ml-auto
                md:ml-0
                ml-auto
                leading-none
                text-sm
                pr-3
                py-1
                border-r-2 border-gray-200
              "
            >
              {{ post.attributes.course_author }}
            </span>
            <span
              class="
                text-gray-400
                inline-flex
                items-center
                leading-none
                text-sm
              "
            >
              {{ post.attributes.course_duration }} hours
            </span>
            <router-link
              :to="{
                name: 'buy',
                params: {
                  id: post.id,
                  name: post.attributes.course_name,
                },
              }"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-6 w-6"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z"
                /></svg
            ></router-link>
          </div>
        </div>
      </div>
    </li>
  </ul>
</template>

<script>
import axios from "axios";
export default {
  created() {
    this.getCategories();
    this.getPosts();
  },
  data() {
    return {
      posts: [],
      categories: [],
      errors: [],
      filtered: [],

      image: "http://localhost:1337",
    };
  },
  methods: {
    async getCategories() {
      await axios
        .get("http://localhost:1337/api/categories?populate=*")
        .then((response) => {
          this.categories = response.data;
        })
        .catch((error) => {
          this.errors.push(error);
        });
    },
    getPosts() {
      axios
        .get("http://localhost:1337/api/courses?populate=*")
        .then((response) => {
          this.posts = response.data;
        })
        .catch((error) => {
          this.errors.push(error);
        });
    },
    showPost(e) {
      if (e === "all") {
        this.getPosts();
      } else {
        axios
          .get("http://localhost:1337/api/courses?populate=*")
          .then((response) => {
            this.posts = response.data;
            this.filtered = this.posts.data.filter((post) => {
              return (
                post.attributes.categories.data[0].attributes.category_name ===
                e
              );
            });
            this.posts.data = this.filtered;
          })
          .catch((error) => {
            this.errors.push(error);
          });
      }
    },
  },
};
</script>
<style scoped>
.image-card {
  border-radius: 2rem;
}

.perspective-left {
  transform: perspective(1500px) rotateY(15deg);
  transition: transform 1s ease 0s;
}

.perspective-left:hover {
  transform: perspective(3000px) rotateY(5deg);
}
</style>