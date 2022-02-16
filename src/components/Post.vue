<template>
  <div class="post" v-for="(data, i) in datas" :key="i">
    <div class="post-header">
      <div
        class="profile"
        v-bind:style="{ backgroundImage: `url(${data.userImage})` }"
      ></div>
      <span class="profile-name">{{ data.name }}</span>
    </div>
    <div
      class="post-body"
      v-bind:style="{ backgroundImage: `url(${data.postImage})` }"
    ></div>
    <div class="post-content">
      <p>Likes {{ data.likes }}</p>
      <p>
        <strong>{{ data.name }}</strong>
        <span>{{ data.content }}</span>
      </p>
      <p class="date">{{ data.date }}</p>
    </div>
  </div>

  <!-- 
  <div class="post">
    <div class="post-header">
      <div class="profile"></div>
      <span class="profile-name">ChanKim</span>
    </div>
    <div class="post-body"></div>
    <div class="post-content">
      <p>43 Likes</p>
      <p><strong>글쓴이아이디</strong> 임시내용</p>
      <p class="date">May 15</p>
    </div>
  </div> -->
</template>

<script>
export default {
  name: "Post",
  props: {
    datas: Array,
  },
};
</script>

<style>
.post {
  width: 100%;
}
.profile {
  width: 30px;
  height: 30px;
  background-size: 100%;
  border-radius: 50%;
  float: left;
}
.profile-name {
  display: block;
  float: left;
  padding-left: 10px;
  padding-top: 7px;
  font-size: 14px;
}
.post-header {
  height: 30px;
  padding: 10px;
}
.post-body {
  height: 450px;
  background-position: center;
  background-size: cover;
}
.post-content {
  padding-left: 15px;
  padding-right: 15px;
  font-size: 14px;
}
.date {
  font-size: 11px;
  color: grey;
  margin-top: -8px;
}
</style>
