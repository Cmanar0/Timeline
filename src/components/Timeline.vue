<template>
  <div class="container">
    <DialogWin v-if="dialogOn" title="Details:" @close="CloseWin">
      <template #default>
        <div class="flex-info">
          <div>
            <p>Name:</p>
            <p>Tags:</p>
            <p>Date:</p>
            <p>Description:</p>
          </div>

          <div>
            <p>{{ dialogContent.name.first }} {{ dialogContent.name.last }}</p>
            <span v-for="tag in dialogContent.tags" :key="tag" :tag="tag">{{ `${tag}, ` }}</span>
            <p>
              {{
                `${dialogContent.myDate.getDate()}, ${
                  this.months[dialogContent.myDate.getMonth()]
                }, ${dialogContent.myDate.getFullYear()}`
              }}
            </p>

            <p>{{ dialogContent.about }}</p>
          </div>
        </div>
      </template>
      <template #actions>
        <button @click="CloseWin">Ok</button>
      </template>
    </DialogWin>
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
          <div v-if="post.myId % 2 == 0" class="content-box" @click="setDialogOn(post)">
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
          </div>
          <div class="left-post-joint">
            <div class="blank"></div>
            <div class="joint"></div>
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
          <div v-if="post.myId % 2 == 1" class="content-box" @click="setDialogOn(post)">
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
          </div>
          <div class="right-post-joint">
            <div class="joint-right"></div>
            <div class="blank"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import DialogWin from './reusable/DialogWin.vue'
import { postsList } from './data.js'
import { iconsList } from './data.js'

export default {
  name: 'HelloWorld',
  components: {
    DialogWin
  },
  data() {
    return {
      dialogOn: false,
      dialogContent: null,
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
    CloseWin() {
      this.dialogOn = false
    },
    setDialogOn(post) {
      this.dialogContent = post
      this.dialogOn = true
    }
  }
}
</script>

<style scoped>
.flex-info {
  text-align: left;
  display: flex;
  gap: 20px;
  justify-content: flex-start;
}
.left-post-joint {
  position: relative;
  display: flex;
  z-index: 10;
  left: 25px;
  bottom: 45px;
  margin-left: auto;
  height: 0;
}
.blank {
  visibility: hidden;
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
  font-size: 25px;

  content: '\f111';
  position: relative;
  left: -50%;
  top: -12px;
  color: rgba(13, 81, 132, 255);
}
.joint-right::after {
  font-family: 'Font Awesome 5 Free';
  font-weight: 900;
  font-size: 25px;
  content: '\f111';
  position: relative;
  right: -50%;
  top: -12px;
  color: rgba(13, 81, 132, 255);
}

.right-post-joint {
  display: flex;
  position: relative;
  z-index: 100;
  right: 22px;
  height: 0;

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
  max-width: 200px;
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
  transform: scale(1);
  transition: 500ms ease-in-out;
  z-index: 250;
  padding: 0 0.6rem;
  cursor: pointer;
  /* background-color: cornsilk; */
}
.content-box:hover {
  transform: scale(1.05);
  transition: 500ms ease-in-out;
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
  font-size: 25px;
  content: '\f111';
  position: relative;
  right: calc(50% + 13.5px);
  top: -7px;
  color: rgba(13, 81, 132, 255);
}
#line::after {
  font-family: 'Font Awesome 5 Free';
  font-weight: 900;
  font-size: 25px;
  content: '\f111';
  color: rgba(13, 81, 132, 255);
  position: relative;
  right: calc(50% + 13.5px);
  top: 7px;
}

.time-line {
  display: flex;
  flex-direction: row;
  z-index: 10;
}
.line {
  border-left: 4px solid rgba(13, 81, 132, 255);
  max-height: calc(auto - 300px);
  position: absolute;
  z-index: 0;
  left: 50%;
  top: 60px;
  width: 1px;
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
