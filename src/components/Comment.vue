<template>
  <div class="comment">
    <div class="avatar">
      <img src="https://placehold.it/150x150">
    </div>
    <div class="comment-body">
      <h4>{{ username }}</h4>
      <p>{{ text }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'comment',
  props: ['text', 'username'],
};
</script>

<style scoped>
* {
  text-align: left;
}
.comment {
  float: left;
  width: 500px;
  border: 1px solid #EEE;
  padding: 15px;
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
</style>
