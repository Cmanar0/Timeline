<template>
  <div class="container">
    <div class="time-line">
      <div class="line" id="line">
        <div v-for="post in postsList" :key="post.id" :post="post" class="invis-height"></div>
      </div>
      <div class="mg-top-26"></div>
      <div v-for="post in postsList" :key="post.id" :post="post" class="time-point">
        <div class="blank"></div>
        <div class="content">
          <div class="content-box">
            <p>
              {{ post._id }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { postsList } from './data.js'

export default {
  name: 'HelloWorld',
  data() {
    return {
      postsList
    }
  },
  methods: {
    aaa() {
      console.log('object')
    }
  }
}
</script>

<style scoped>
.content-box {
  padding: 15px;
}
.time-point {
  padding: 30px;
  height: 100px;
  display: flex;
  z-index: 50;
  width: 100%;
  position: relative;
  border: 1px solid red;
}
.blank {
  width: 50%;
}
.content {
  width: 50%;
}
.invis-height {
  height: 158px;
  border: 1px solid red;
  width: 50vw;
  position: relative;
  visibility: hidden;
}
#line::before {
  font-family: 'Font Awesome 5 Free';
  font-weight: 900;
  content: '\f111';
  position: relative;
  right: calc(50% + 1px);
  top: -7px;
  color: rgba(13, 81, 132, 255);
}
#line::after {
  font-family: 'Font Awesome 5 Free';
  font-weight: 900;
  content: '\f111';
  color: rgba(13, 81, 132, 255);
  position: relative;
  right: calc(50% + 1px);
  top: 7px;
}
.time-line .bottom-p {
  position: relative;
  left: -9px;
  top: calc(auto - 20px);
}
.point {
  height: 15px;
  width: 15px;
  background-color: rgba(13, 81, 132, 255);
  border-radius: 50%;
}
.time-line {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.line {
  border-left: 4px solid rgba(13, 81, 132, 255);
  height: calc(auto - 40px);
  position: absolute;
  left: 50%;
  top: 20px;
  margin-left: -3px;
}
.container {
  padding: 15px;
}
p {
  margin: 0;
}
</style>
<style>
#app {
  margin: 0;
}
body {
  margin: 0;
  padding: 0;
  font-family: Roboto, basic-sans, sans-serif;
}
.mg-top-10 {
  margin-top: 10px;
}
.mg-top-15 {
  margin-top: 15px;
}
.mg-top-20 {
  margin-top: 20px;
}
.mg-top-26 {
  margin-top: 26px;
}
.mg-bot-10 {
  margin-bottom: 10px;
}
.mg-bot-15 {
  margin-bottom: 15px;
}
.mg-bot-20 {
  margin-bottom: 20px;
}
</style>
