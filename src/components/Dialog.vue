<template>
  <div class="dialog-bg">
    <div class="dialog">
      <div class="header">
        <div class="title">{{title}}</div>
    </div>
    <div class="container">
      <div class="message">
        {{message}}
      </div>
    </div>
    <div class="footer">
      <button class="closeBtn" @click="close">Close</button>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Dialog',
  props: ['title', 'message'],
  data () {
    return {
      flag: true
    }
  },
  methods: {
    close () {
      this.$emit('closeDialog', false)
    }
  }
}
</script>

<style scoped>
.dialog-bg {
  position: fixed;
  top: 0%;
  left: 0%;
  width: 100vw;
  height: 100vh;
  text-align: center;
  background-color: rgba(0, 0, 0, 0.5);
}
.dialog {
  margin: 0px;
  padding: 0px;
  width: 300px;
  height: 200px;
  background-color: white;
  border-radius: 5px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  /* display: flex; */
  /* flex-direction: column; */
  text-align: center;
  vertical-align:middle;
}
.header {
  height: 50px;
  /* flex-basis: 50px; */
  /* flex-shrink: 0; */
  display: flex;
  justify-content: center;
  align-items: center;
  border-bottom: 1px solid #cdcdcd;
}
.container {
  height: 98px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-bottom: 1px solid #cdcdcd;
}
.footer {
  height: 50px;
  /* flex-basis: 50px; */
  /* flex-shrink: 0; */
  display: flex;
  justify-content: center;
  align-items: center;
}
.closeBtn {
  outline: none;
  width: 82px;
  height: 32px;
  font-size: 16px;
  font-weight: bolder;
  background-color: rgba(44, 118, 255, 0.822);
  border: 1px solid white;
  border-right: 1px solid #cdcdcd;
  border-bottom: 1px solid #cdcdcd;
  border-radius: 5px;
}
.closeBtn:hover {
  background-color: cadetblue;
  color: #cdcdcd;
  border-left: 1px solid #cdcdcd;
  border-top: 1px solid #cdcdcd;
}
</style>
