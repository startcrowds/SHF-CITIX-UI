<template>
    <div class="vue-tempalte">
        <ul v-if="posts && posts.length">
      <li v-for="post of posts" v-bind:key="post">
        <p><strong>{{post.name}}</strong></p>
        <p>{{post.location}}</p>
		<p>{{post.rating}}</p>
      </li>
    </ul>

    <ul v-if="errors && errors.length">
      <li v-for="error of errors" v-bind:key="error">
        {{error.message}}
      </li>
    </ul>
    </div>
	
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      posts: [],
      errors: []
    }
  },

  // Fetches posts when the component is created.
  created() {
    axios.get(`https://969rgz78f9.execute-api.us-east-1.amazonaws.com/dev/api/stores`)
    .then(response => {
      // JSON responses are automatically parsed.
      this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>