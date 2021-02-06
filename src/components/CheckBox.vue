<template>
  <div :class="result?'check-box':'check-box error'">
    <a>* </a><a>{{question}}</a><a style="color: grey;">【请选择{{min}}-{{max}}项】</a>
    <div>
      <ul>
        <label v-for="(item, id) in data" v-bind:key="id">
          <li>
            <input type="checkbox" v-model="item.checked" ref="checkBox" @change="listenMorethanMax(item)"/>{{item.name}}
          </li>
        </label>
      </ul>
      <div class="result">您已经选择了{{max>=selectItemCount?selectItemCount:max}}项<a v-if="selectItemCount<min?true:false">，少选择了{{selectItemCount===0?min:max-selectItemCount}}项</a></div>
      <Dialog v-if="showDialog" :title="title" :message="message"  @closeDialog="close"></Dialog>
    </div>
  </div>
</template>

<script>
import Dialog from '@/components/Dialog'
export default {
  name: 'CheckBox',
  props: ['items', 'question', 'max', 'min', 'submit', 'result'],
  components: {
    Dialog
  },
  data () {
    return {
      data: this.items,
      showDialog: false,
      title: '系统提示',
      message: `此题最多只能选择${this.max}项`
    }
  },
  methods: {
    listenMorethanMax (i) {
      let count = this.data.filter(item => item.checked)
      if (count.length > this.max) {
        this.data.forEach(item => {
          if (i.id === item.id) {
            item.checked = false
            let checkboxes = document.querySelectorAll('input[type="checkbox"]')
            checkboxes[i.id - 1].checked = false
            this.showDialog = true
          }
        })
      }
    },
    close () {
      this.showDialog = false
    },
    testNotNull () {
      let count = this.data.filter(item => item.checked).length
      if (count >= this.min) {
        console.log('54')
        this.$emit('checkbox', true)
      } else {
        this.$emit('checkbox', false)
      }
    }
  },
  computed: {
    selectItemCount: function () {
      let count = this.data.filter(item => item.checked)
      return count.length
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
  .check-box {
    width:inherit;
    margin: 15px 0px;
    border: 1px solid white;
  }
  .error {
    border: 1px solid orange;
  }
  .check-box a:nth-of-type(2){
    font-weight: bold;
  }

  a:first-of-type {
    color:red;
  }
  ul {
    width: 100%;
    list-style: none;
    display: flex;
    flex-wrap: wrap;
    margin: 0px;
    padding: 0px;
  }
  label {
    flex-basis: 50%;
  }
  li:hover{
    background-color: #cdcdcd;
  }
  .result a {
    color: red;
  }
</style>
