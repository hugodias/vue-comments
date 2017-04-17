<template>
  <div class="comment" v-bind:class="[isParent() ? parentClass : childrenClass]">
    <div class="avatar">
      <img src="https://placehold.it/150x150">
    </div>
    <div class="comment-body">
      <div class="text">
        <h4>{{ username }}</h4>
        <time>{{ created_at | moment("MMMM Do YYYY, h:mm:ss a") }}</time>
        <p>{{ text }}</p>
      </div>

      <footer>
        <div class="actions">
          <a v-on:click="like" v-if="!liked">Like</a>
        </div>
        <div class="info">
          {{ score }} likes .
          <span v-if="isParent()">
            {{ replies.length }} replies .
          </span>
        </div>
      </footer>

      <div v-if="isParent()" class="reply">
        <input type="text" v-model="replyText" v-on:keyup.enter="reply">
        <button v-on:click="reply">Reply</button>

        <div class="replies">
          <comment v-for="children in replies"
                   :key="children"
                   :id="children.id"
                   :text="children.text"
                   :created_at="children.created_at"
                   :username="children.username"
                   :likes="children.likes"
                   :comment_type="'child'"></comment>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'comment',
  props: ['id', 'text', 'username', 'created_at', 'comment_type', 'likes'],
  data() {
    return {
      parentClass: 'parent',
      childrenClass: 'children',
      replyText: '',
      score: this.likes,
      liked: false,
      replies: [],
    };
  },
  created() {
    if (this.isParent()) {
      this.fetchReplies();
    }
  },
  methods: {
    isParent() {
      return this.comment_type === 'parent';
    },
    like() {
      if (!this.liked) {
        this.score += 1;
        this.liked = true;
      }
    },
    reply() {
      this.replies.push({
        id: this.replies.length + 1,
        text: this.replyText,
        username: 'Hugo Dias',
        created_at: Date.now(),
        likes: 0,
      });

      this.replyText = '';
    },
    fetchReplies() {
      const apiURL = `https://demo1299998.mockable.io/comments/${this.id}`;
      const self = this;

      this.$http.get(apiURL).then((response) => {
        self.replies = response.body;
      }, (response) => {
        console.log(response);
      });
    },
  },
};
</script>

<style scoped>
.comment {
  text-align: left;
  float: left;
  width: 100%;
  border: 1px solid #EEE;
  padding: 15px;
  margin-bottom: 20px;
}
.comment.children{
  margin-bottom: 5px;
}
.text {
  float: left;
  width: 100%;
}
.avatar {
  float: left;
  width: 70px;
}

.comment-body {
  float: left;
  width: 80%;
}
.avatar img {
  width: 50px;
  height: 50px;
}
h4 {
  margin: 0;
}
p {
  margin: 0;
  font-size: 14px;
  float: left;
}
footer {
  float: left;
  width: 100%;
  height: 20px;
  padding-top: 13px;
  padding-bottom: 10px;
}
a {
  font-weight: bold;
  cursor: pointer;
}
time {
  font-size: 11px;
  margin-bottom: 8px;
  width: 100%;
  float: left;
}
.actions {
  float: left;
}
.info {
  float: right;
}
.reply {
  border-top: 1px solid #EEE;
  width: 100%;
  float: left;
  padding-top: 10px;
}
.replies {
  margin-top: 20px;
}
input {
  float: left;
  margin-bottom: 20px;
  height: 30px;
  padding-left: 10px;
  border: 1px solid #EEE;
  width: 80%;
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
</style>
