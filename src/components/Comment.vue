<template>
  <div class="comment">
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
          {{ likes }} likes .
          {{ replies.length }} replies .
        </div>
      </footer>
      <div class="reply">
        <input type="text">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'comment',
  props: ['text', 'username', 'created_at'],
  data() {
    return {
      likes: 0,
      liked: false,
      replies: [],
    };
  },
  methods: {
    like() {
      if (!this.liked) {
        this.likes += 1;
        this.liked = true;
      }
    },
  },
};
</script>

<style scoped>
.comment {
  text-align: left;
  float: left;
  width: 500px;
  border: 1px solid #EEE;
  padding: 15px;
  margin-bottom: 20px;
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
  width: 430px;
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
  border-bottom: 1px solid #EEE;
  padding-bottom: 10px;
  margin-bottom: 10px;
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
</style>
