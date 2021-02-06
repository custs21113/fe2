<template>
<div>
  <div :class="result?'multi-radio':'multi-radio error'">
    <div style="width: 100%" >
      <a>*</a>
      <a>您现在的年级是</a>
      <div class="options">
        <label v-for="(item, index) in items" v-bind:key="index" :for="index">
          <input type="radio" v-model="question3" name="question3" :id="index" :value="item.value" />{{item.grade}}
        </label>
      </div>
    </div>
  </div>
  <CheckBox v-show="question3===5||question3===6" :items="childItems" :question="question" :max="max" :min="min" :result="checkboxSubmit===0?true:checkboxResult" @checkbox="testCheckBox" :submit="checkboxSubmit"></CheckBox>
</div>
</template>
<script>
import CheckBox from '@/components/CheckBox'
export default {
  name: 'MultiRadio',
  props: ['submit', 'result'],
  components: {
    CheckBox
  },
  data () {
    return {
      items: [
        {
          value: 1,
          grade: '大一'
        },
        {
          value: 2,
          grade: '大二'
        },
        {
          value: 3,
          grade: '大三'
        },
        {
          value: 4,
          grade: '大四'
        },
        {
          value: 5,
          grade: '硕士'
        },
        {
          value: 6,
          grade: '博士'
        }],
      childItems: [
        {
          id: 1,
          name: 'test',
          checked: false
        },
        {
          id: 2,
          name: 'TT',
          checked: false
        },
        {
          id: 3,
          name: 'TT',
          checked: false
        },
        {
          id: 4,
          name: 'TT',
          checked: false
        },
        {
          id: 5,
          name: 'TT',
          checked: false
        }
      ],
      question: '您在毕业后关于行业优先考虑的因素有？',
      question3: '',
      checkboxResult: false,
      checkboxSubmit: this.submit,
      max: 3,
      min: 1,
      grade: []
    }
  },
  methods: {
    testNotNull () {
      if (this.question3 === 5 || this.question3 === 6) {
        if (this.checkboxResult) {
          console.log(92)
          this.$emit('question3', true)
        } else {
          this.$emit('question3', false)
        }
      } else {
        if (this.question3 !== '') {
          console.log(99)
          this.$emit('question3', true)
        } else {
          this.$emit('question3', false)
        }
      }
    },
    testCheckBox (data) {
      console.log(103, data)
      if (data) {
        this.checkboxResult = true
      } else {
        this.checkboxResult = false
      }
    }
  },
  watch: {
    submit: {
      handler: function () {
        this.testNotNull()
        this.checkboxSubmit++
      }
    },
    checkboxResult: {
      handler: function () {
        this.$nextTick(() => {
          this.testNotNull()
        })
      }
    }
  }
}
</script>
<style scoped>
.multi-radio {
  display: block;
  list-style: none;
  width: inherit;
  margin: 15px 0px;
  border: 1px solid white;
}
.error {
  border: 1px solid orange;
}
a:first-of-type {
  color: red;
}
.multi-radio a {
  font-weight: bold;
}
.options {
  width: 100%;
  list-style: none;
  display: flex;
  flex-wrap: wrap;
}
label {
  line-height: 30px;
  display: inline;
  flex-basis: 50%;
  flex-grow: 1;
  flex-shrink: 0;
}
label:hover {
  background-color: #cdcdcd;
}
</style>
