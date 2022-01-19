<template>
  <div class="container">
    <div class="time-line">
      <div class="line" id="line">
        <div v-for="post in myPostsList" :key="post.id" :post="post" class="invis-height"></div>
      </div>
      <div class="mg-top-26"></div>
      <div v-for="post in myPostsList" :key="post.id" :post="post" class="time-point">
        <div class="content">
          <div v-if="post.myID % 2 == 1" class="content-box">
            <i :class="post.randomIcon"></i>
            <div class="date">
              <p>
                {{ post.registered }}
              </p>
            </div>
            <div class="name">
              <p>
                {{ post.name.first }}
                {{ post.name.last }}
              </p>
            </div>
            <div class="shorten-flex">
              <div class="shorten-text">
                {{ post.about }}
              </div>
            </div>
          </div>
          <div v-else></div>
        </div>
        <div class="content">
          <div v-if="post.myID % 2 == 0" class="content-box">
            <i :class="post.randomIcon"></i>
            <div class="date">
              <p>
                {{ post.registered }}
              </p>
            </div>
            <div class="name">
              <p>
                {{ post.name.first }}
                {{ post.name.last }}
              </p>
            </div>
            <div class="shorten-flex">
              <div class="shorten-text">
                {{ post.about }}
              </div>
            </div>
          </div>
          <div v-else></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { postsList } from './data.js'
import { iconsList } from './data.js'

export default {
  name: 'HelloWorld',
  data() {
    return {
      postsList,
      iconsList,
      myPostsList: null,
      iconsListRandom: null
    }
  },

  created() {
    function getRandom(min, max) {
      return Math.floor(Math.random() * (max - min)) + min
    }
    this.myPostsList = [...this.postsList]
    for (let i = 0; i < this.myPostsList.length; i++) {
      this.myPostsList[i]['myID'] = i
      let num = getRandom(1, 15)
      this.myPostsList[i]['randomIcon'] = this.iconsList[num]
    }
    console.log(this.myPostsList)
  },
  methods: {
    aaa() {
      console.log('object')
    }
  }
}
</script>

<style scoped>
.date {
  font-size: 20px;
  font-weight: 700;
  color: rgba(13, 81, 132, 255);
}
.name {
  font-size: 20px;
}
.shorten-text {
  white-space: nowrap;
  overflow: hidden;
  width: 80%;
  text-overflow: ellipsis;
  font-size: 18px;
}
.shorten-flex {
  display: flex;
  justify-content: center;
}
.icon {
  font-size: 30px;
}
.content-box {
  padding: 0 15px 0 15px;
}
.time-point {
  padding: 15px;
  height: 130px;
  display: flex;
  z-index: 50;
  width: 80%;
  position: relative;
  top: -50px;
  border: 1px solid red;
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
  padding: 0 15px 15px 15px;
}
p {
  margin: 0;
}
@media (min-width: 750px) {
}
</style>
<style>
#app {
  margin: 0;
}
body {
  width: 100%;
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
