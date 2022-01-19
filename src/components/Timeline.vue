<template>
  <div class="container">
    <div class="line" id="line">
      <div v-for="post in myPostsList" :key="post.id" :post="post" class="invis-height"></div>
    </div>
    <div class="time-line">
      <div class="left-column">
        <div class="mg-top-50"></div>
        <div
          v-for="post in myPostsList"
          :key="post.id"
          :post="post"
          class="box mg-right-15"
          :class="{ none: post.myId % 2 == 1 }"
        >
          <div v-if="post.myId % 2 == 0" class="content-box">
            <i :class="post.randomIcon"></i>
            <div class="date">
              <p>
                {{ `${post.myDate.getDate()} ${this.months[post.myDate.getMonth()]}` }}
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
            <div class="left-post-joint">
              <div class="blank"></div>
              <div class="joint"></div>
            </div>
          </div>
        </div>
      </div>
      <div class="right-column">
        <div class="mg-top-90"></div>
        <div
          v-for="post in myPostsList"
          :key="post.id"
          :post="post"
          class="box mg-left-15"
          :class="{ none: post.myId % 2 == 0 }"
        >
          <div v-if="post.myId % 2 == 1" class="content-box">
            <i :class="post.randomIcon"></i>
            <div class="date">
              <p>
                {{ `${post.myDate.getDate()} ${this.months[post.myDate.getMonth()]}` }}
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
            <div class="right-post-joint">
              <div class="joint-right"></div>
              <div class="blank"></div>
            </div>
          </div>
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
      months: ['Jan', 'Fer', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
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
      let str = this.myPostsList[i].registered.replace(/,/g, '')
      let date = new Date(str)
      this.myPostsList[i]['myDate'] = date

      this.myPostsList[i]['myId'] = i
      let num = getRandom(1, 15)
      this.myPostsList[i]['randomIcon'] = this.iconsList[num]
    }
    // console.log(this.myPostsList)
  },
  methods: {
    aaa() {
      console.log('object')
    }
  }
}
</script>

<style scoped>
.left-post-joint {
  position: relative;
  display: flex;
  z-index: 100;
  left: 33px;
  bottom: 45px;
  margin-left: auto;
}
.blank {
  border: 2px solid rgba(13, 81, 132, 255);
  height: 0;
  width: 80%;
  opacity: 0;
}
.joint {
  border: 2px solid rgba(13, 81, 132, 255);
  height: 0;
  width: 20%;
  background-color: rgba(13, 81, 132, 255);
}
.joint-right {
  border: 2px solid rgba(13, 81, 132, 255);
  height: 0;
  width: 20%;
  background-color: rgba(13, 81, 132, 255);
}
.joint::before {
  font-family: 'Font Awesome 5 Free';
  font-weight: 900;
  content: '\f111';
  position: relative;
  left: -50%;
  top: -10px;
  color: rgba(13, 81, 132, 255);
}
.joint-right::after {
  font-family: 'Font Awesome 5 Free';
  font-weight: 900;
  content: '\f111';
  position: relative;
  right: -50%;
  top: -10px;
  color: rgba(13, 81, 132, 255);
}
.right-post-joint {
  display: flex;
  position: relative;
  z-index: 100;
  right: 30px;
  bottom: 45px;
  margin-right: auto;
}
.none {
  display: none;
}
.left-column {
  width: 50%;
  display: flex;
  flex-direction: column;
}
.right-column {
  width: 50%;
  display: flex;
  flex-direction: column;
}
.box {
  min-height: 140px;
  max-height: 175px;
  padding: 1rem 0.5rem;
  /* border: 1px solid slategrey; */
}
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
  padding: 0 0.6rem;
}

.invis-height {
  height: 85px;
  border: 1px solid red;
  width: 50vw;
  position: relative;
  visibility: hidden;
}
.invis-height-short {
  height: 20px;
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

.time-line {
  display: flex;
  flex-direction: row;
}
.line {
  border-left: 4px solid rgba(13, 81, 132, 255);
  max-height: calc(auto - 300px) !important;
  position: absolute;
  left: 50%;
  top: 60px;
}
.container {
  padding: 0.5rem;
  padding-top: 0;
}
p {
  margin: 0;
}
.mg-left-15 {
  margin-left: 15px;
}
.mg-right-15 {
  margin-right: 15px;
}
</style>
<style>
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
.mg-top-50 {
  margin-top: 50px;
}
.mg-top-90 {
  margin-top: 140px;
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
