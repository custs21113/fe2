<template>
    <div :class="result?'question':'question error'">
      <span>* </span>
      <div>
        姓名: <input v-model="name" type="text" />
        年龄: <input v-model="age" type="text" style="width:20px" min="0"/> 岁<br/>
        电话: <input v-model="phone" type="number"/>
      </div>
    </div>
</template>
<script>
export default {
  name: 'Question',
  props: ['submit', 'result'],
  data () {
    return {
      name: '',
      age: '',
      phone: ''
    }
  },
  methods: {
    testNotNull () {
      if (this.name !== '' && this.age !== '' && this.phone !== '') {
        this.$emit('question1', true)
      } else {
        this.$emit('question1', false)
      }
    }
  },
  watch: {
    submit: {
      handler: function () {
        this.testNotNull()
      }
    }
  }
}
</script>
<style scoped>
  .question {
    width: 100%;
    display: inline-flex;
    margin: 15px 0px;
    font-weight: bold;
    border: 1px solid white;
  }
  .error {
    border: 1px solid orange;
  }
  span:first-child {
    color: red;
    display: inline-block;
    width: 5px;
  }
  input{
    outline: none;
    border: 1px solid transparent;
    border-bottom: 1px solid #cdcdcd;
    width: 30%;
  }
  input:hover {
    border: 1px solid #cdcdcd;
  }
</style>
