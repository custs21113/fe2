<template>
  <div :class="result?'radio':'radio error'">
    <a>* </a>
    <a>您的性别是</a>
    <li>
      <label> <input type="radio" v-model="radioResult" name="question2" value="1" />男 </label>
    </li>
    <li>
      <label> <input type="radio" v-model="radioResult" name="question2" value="2" />女 </label>
    </li>
  </div>
</template>
<script>
export default {
  name: 'Radio',
  props: ['submit', 'result'],
  data () {
    return {
      radioResult: ''
    }
  },
  methods: {
    testNotNull () {
      if (this.radioResult) {
        this.$emit('question2', true)
      } else {
        this.$emit('question2', false)
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
.radio {
  margin: 15px 0px ;
  list-style: none;
  border: 1px solid white;
}
.error {
  border: 1px solid orange;
}
.radio a{
  font-weight: bold;
}
a:first-of-type {
  color: red;
}
label {
  display: block;
  line-height: 30px;
}
label:hover{
  background-color: #cdcdcd;
}

</style>
