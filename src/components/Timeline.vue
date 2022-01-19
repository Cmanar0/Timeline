<template>
  <div>
    <div class="time-line">
      <div class="line" id="line">
        <div><p>sadasdads</p></div>
        <div><p>sadasdads</p></div>
        <div><p>sadasdads</p></div>
        <div><p>sadasdads</p></div>
        <div><p>sadasdads</p></div>
        <div><p>sadasdads</p></div>
        <div><p>sadasdads</p></div>
        <div><p>sadasdads</p></div>
        <div><p>sadasdads</p></div>
        <div><p>sadasdads</p></div>
        <div><p>sadasdads</p></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#line::before {
  font-family: 'Font Awesome 5 Free';
  font-weight: 900;
  content: '\f007';
  position: relative;
  left: -50px;
  top: 0;
}
#line::after {
  font-family: 'Font Awesome 5 Free';
  font-weight: 900;
  content: '\f015';
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
}
.line {
  border-left: 4px solid rgba(13, 81, 132, 255);
  height: calc(auto - 40px);
  position: absolute;
  left: 50%;
  top: 20px;
  margin-left: -3px;
}
</style>
