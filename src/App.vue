<template>
  <div class="container mx-auto py-10 flex space-x-10">
    <div class="sidebar flex flex-col space-y-2">
      <p>Sidebar</p>

      <input
        class="
          py-1
          px-2
          bg-stone-100
          rounded-md
          outline-none
          focus:ring-1
          ring-stone-500
        "
        type="text"
        v-model="search"
        placeholder="type post title ..."
      />
    </div>

    <list :posts="searchPost" />
    <div>
      <div class="h-10">
        <p v-if="show" class="mb-5 bg-gray-500 border-gray-700 w-20">
          {{ title }}
        </p>
      </div>
      <button
        @mouseover="mouse($event, 5)"
        class="border-2 border-red-500 w-20"
        @click="toggle"
      >
        <span>hide it</span>
      </button>
      <div >
          <ul>
              <li :key="book.id" v-for="book in books">
                  <img :src="book.img" :alt="book.title">
              </li>
          </ul>
      </div>

      <button
        @mousemove="ofset($event)"
        class="border-2 border-red-500 w-40 m-5 h-10"
        @click="toggle"
      >
        <span>{{ x }}-{{ y }}</span>
      </button>
    </div>
  </div>
</template>

<script>
import List from "./components/List.vue";
import axios from "axios";
export default {
  components: {
    List,
  },
  data() {
    return {
      search: "",
      posts: [],
      title: "razi",
      show: true,
      books: [
        {
          title: "hello",
          img: "src/assets/img/1.jpeg",
        },
        {
          title: "hello2",
          img: "src/assets/img/2.jpeg",
        },
        {
          title: "hello2",
          img: "src/assets/img/2.jpeg",
        },
      ],
      x: "",
      y: "",
    };
  },

  async mounted() {
    console.log(this);
    await axios
      .get("https://jsonplaceholder.typicode.com/posts")
      .then((response) => (this.posts = response.data));
  },
  methods: {
    toggle() {
      this.show = !this.show;
    },
    mouse(e, data) {
      console.log(e, e.type);
      if (data) {
        console.log(data);
      }
    },
    ofset(e) {
      this.x = e.offsetY;
      this.y = e.offsetX;
    },
  },
  computed: {
    searchPost() {
      // return this.posts;
      return this.posts.filter((item) =>
        item.title.includes(this.search.toLowerCase())
      );
    },
  },
};
</script>
