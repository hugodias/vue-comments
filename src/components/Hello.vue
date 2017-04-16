<template>
  <div class="hello">
    <div class="comments">
      <input v-model="message" v-on:keyup.enter="saveMessage" placeholder="Comment here">
      <button v-on:click="saveMessage">Comment</button>
      <hr/>
      <comment
         v-for="comment in comments"
         :key="comment"
         :id="comment.id"
         :text="comment.text"
         :created_at="comment.created_at"
         :username="comment.username"
         :comment_type="'parent'"></comment>
    </div>

  </div>
</template>

<script>
import Comment from '@/components/Comment';

const apiURL = 'https://demo1299998.mockable.io/comments';

export default {
  name: 'hello',
  created() {
    this.fetchData();
  },
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
    fetchData() {
      const self = this;

      this.$http.get(apiURL).then((response) => {
        self.comments = response.body;
      }, (response) => {
        console.log(response);
      });
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
