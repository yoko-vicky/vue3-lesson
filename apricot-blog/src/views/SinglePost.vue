<template>
  <div v-if="error">{{ error }}</div>
  <div v-if="post" class="post">
    <h1>{{ post.title }}</h1>
    <p class="pre">{{ post.body }}</p>
    <span v-for="tag in post.tags" :key="tag">
      <router-link :to="{ name: 'Tag', params: { tag: tag } }"
        >#{{ tag }}
      </router-link>
    </span>
  </div>
  <div v-else><Spinner /></div>
</template>

<script>
import getPost from '../composables/getPost';
import Spinner from '../components/Spinner.vue';
import { useRoute } from 'vue-router';

export default {
  name: 'SinglePost',
  props: ['id'],
  components: { Spinner },
  setup(props) {
    const route = useRoute();
    // console.log(route);
    // const { post, error, load } = getPost(props.id);
    const { post, error, load } = getPost(route.params.id);
    load();

    return {
      post,
      error,
    };
  },
};
</script>

<style>
.tags a {
  margin-right: 10px;
}
.post {
  max-width: 1200px;
  margin: 0 auto;
}
.post p {
  color: #444;
  line-height: 1.5em;
  margin-top: 40px;
}
.pre {
  white-space: pre-wrap;
}
</style>
