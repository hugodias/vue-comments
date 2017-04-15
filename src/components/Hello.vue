<template>
  <div class="hello">
    <div class="comments">
      <input v-model="message" v-on:keyup.enter="saveMessage" placeholder="Comment here">
      <button v-on:click="saveMessage">Comment</button>
      <hr/>
      <comment
         v-for="comment in comments"
         v-bind:key="comment"
         v-bind:text="comment.text"
         v-bind:created_at="comment.created_at"
         v-bind:username="comment.username"
         v-bind:comment_type="'parent'"></comment>
    </div>

  </div>
</template>

<script>
import Comment from '@/components/Comment';

export default {
  name: 'hello',
  methods: {
    saveMessage() {
      this.comments.push({
        id: this.comments.lenght + 1,
        text: this.message,
        username: 'Hugo Dias',
        created_at: Date.now(),
      });

      this.message = '';
    },
  },
  data() {
    return {
      message: '',
      comments: [],
    };
  },
  components: {
    Comment,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.comments {
  width: 530px;
  margin: 0 auto;
}

input {
  float: left;
  width: 420px;
  margin-bottom: 20px;
  height: 30px;
  padding-left: 10px;
  border: 1px solid #EEE;
}

input:hover,
input:focus {
  outline: none;
}

button {
  float: right;
  background-color: #42b983;
  color: #FFF;
  border: 1px solid #35495E;
  padding: 10px 15px;
  font-weight: bold;
}
hr {
  clear: both;
  border: 1px solid #EEE;
  margin-bottom: 20px;
}
</style>
