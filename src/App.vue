<template>
  <div class="header">
    <ul class="header-button-left">
      <li>Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li @click="step = 2" v-if="step === 1">Next</li>
      <li @click="uploadPost" v-if="step === 2">Upload</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>

  <button @click="stpeChange(0)">포스트</button>
  <button @click="stpeChange(1)">포스트 필터 편집</button>
  <button @click="stpeChange(2)">포스트 텍스트 편집</button>

  <Container
    @inputText="getInputText"
    :datas="datas"
    :step="step"
    :ImageURL="ImageURL"
  />

  <div class="footer">
    <ul class="footer-button-plus">
      <input
        @change="upload"
        multiple
        type="file"
        id="file"
        class="inputfile"
      />
      <label for="file" class="input-plus">+</label>
    </ul>
  </div>
</template>

<script>
import Container from "./components/Container.vue";
import postData from "./api/postData";
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      datas: postData,
      step: 0,
      ImageURL: "",
      text: "",
    };
  },
  components: {
    Container,
  },
  methods: {
    more() {
      axios
        .get(`https://codingapple1.github.io/vue/more${this.count}.json`)
        .then((res) => {
          this.datas.push(res.data);
          this.count++;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    stpeChange(num) {
      this.step = num;
    },
    upload(e) {
      const uploadedFile = e.target.files[0];
      console.log(uploadedFile.type);
      this.step = 1;
      this.ImageURL = URL.createObjectURL(uploadedFile);
    },
    uploadPost() {
      const newPost = {
        name: "Kim Hyun",
        userImage: "https://placeimg.com/100/100/arch",
        postImage: `${this.ImageURL}`,
        likes: 33,
        date: "May 15",
        liked: false,
        content: `${this.text}`,
        filter: "perpetua",
      };
      this.datas.unshift(newPost);
      this.step = 0;
    },
    getInputText(text) {
      this.text = text;
    },
  },
};
</script>

<style>
.hide {
  display: none;
}

body {
  margin: 0;
}
ul {
  padding: 5px;
  list-style-type: none;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: white;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}
.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
}
#app {
  box-sizing: border-box;
  font-family: "consolas";
  margin-top: 60px;
  width: 100%;
  max-width: 460px;
  margin: auto;
  position: relative;
  border-right: 1px solid #eee;
  border-left: 1px solid #eee;
}
</style>
