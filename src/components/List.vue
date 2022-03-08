<template>
  <div class="w-full space-y-4">
    <Loading v-if="posts.length < 1"/>
    <div  v-else v-for="post in posts" :key="post.id" class="bg-stone-300 shadow-md rounded-lg py-4 px-2">
      <div>
        <span>Id:</span>
        {{ post.id }}
      </div>
      <div>
        <span>Title:</span>
        {{ post.title }}
      </div>
      <div>
        <span>Body:</span>
        {{ post.body }}
      </div>
    </div>
  </div>
</template>
<script>
import Loading from "./Loading.vue"
export default {
  props: ["posts"],
  components: { Loading}
  
};

</script>