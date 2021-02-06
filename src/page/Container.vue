<template>
  <div class="container">
    <div class="header">
      <div class="title">
        海康威视实习生编程题<img class="img" src="https://qr.wjx.cn/handler/qrcode.ashx?chl=https%3a%2f%2fwww.wjx.cn%2fvm%2frBmQ3hC.aspx&chs=50x50&sign=0968f63e1f98d30d26ea3adadbf0ae3446bfa3c1" />
      </div>
    </div>
    <Tip class="tip"></Tip>
    <div style="margin: 15px 80px;">
      <Question :submit="submit" :result="submit===0?true:question1Result" @question1="testQuestion"></Question>
      <Radio :submit="submit" :result="submit===0?true:question2Result" @question2="testQuestion2"></Radio>
      <MultiRadio :submit="submit" :result="submit===0?true:question3Result" @question3="testQuestion3"></MultiRadio>
    </div>
    <div class="footer">
      <input type="button" value="提交" class="submitBtn" @click="submitFunc"/>
    </div>
    <Dialog v-if="showDialog" :title="title" :message="message" @closeDialog="close"></Dialog>
    <div class="bottom">
      <hr/>
      问卷星 提供技术支持
    </div>
  </div>
</template>
<script>
import Question from '@/components/Question'
import Tip from '@/components/Tip'
import Radio from '@/components/Radio'
import MultiRadio from '@/components/MultiRadio'
import Dialog from '@/components/Dialog'
export default {
  components: {
    Tip,
    Question,
    Radio,
    MultiRadio,
    Dialog
  },
  data () {
    return {
      submit: 0,
      sum: 0,
      title: '',
      message: '',
      question1Result: false,
      question2Result: false,
      question3Result: false,
      showDialog: false
    }
  },
  methods: {
    submitFunc () { /* 触发后进行表单输入验证，成功则完成提交 */
      this.submit++
      this.finallySubmint()
    },
    close () {
      this.showDialog = false
    },
    finallySubmint () {
      if (this.sum < 3) {
        this.showDialog = true
        this.title = '操作结果'
        this.message = `问卷还未完成，请完成后再提交。`
        this.sum = 0
      } else {
        this.showDialog = true
        this.title = '操作结果'
        this.message = `成功提交。`
        this.sum = 0
      }
    },
    testQuestion (data) {
      if (data) {
        console.log(71)
        this.question1Result = true
        this.sum = this.sum + 1
      } else {
        this.question1Result = false
      }
    },
    testQuestion2 (data) {
      if (data) {
        console.log(88)
        this.question2Result = true
        this.sum = this.sum + 1
      } else {
        this.question2Result = false
      }
    },
    testQuestion3 (data) {
      if (data) {
        console.log(89)
        this.question3Result = true
        this.sum = this.sum + 1
      } else {
        this.question3Result = false
      }
    }
  },
  watch: {
    sum: {
      handler: function () {
        if (this.sum === 3) {
          this.finallySubmint()
        }
      }
    }
  }
}
</script>
<style scoped>
.container {
  width: 70vw;
  height: auto;
  margin-top: 100px;
  padding-bottom: 20px;
  text-align: left;
  background-color: rgb(255, 255, 255);
  border-radius: 5px;
}
.header {
  margin: 10px 0px;
  width: 100%;
  display: inline-block;
  /* background-color: yellow; */
  position: relative;
}
.title {
  font-size: 24px;
  font-weight: bold;
  text-align: center;
  color: #0095ff;
  padding:15px 0;
}
.img{
  position: absolute;
  left: calc(100% - 50px);
  bottom: 5px;
  border: none;
  outline: none;
  width: 50px;
  height: 50px;
  background-color: yellow;
}
.tip {
  margin: 0 80px;
}
.submitBtn{
  background-color:#0095ff;
  color: white;
  outline: none;
  width: 82px;
  height: 32px;
  font-size: 16px;
  border: none;
  border-radius: 1px;
}
.submitBtn:hover{
  background-color: blue;
}
.footer {
  display: block;
  text-align: center;
}
.bottom {
  display: block;
  text-align: center;
}
</style>
