<template>
  <div id="app">
    <test 
      v-for="(msg, index) in messages"
      v-bind:message="msg"
      v-bind:index="index"
      :key="index"
    ></test>
    <hr />
    <button v-on:click="getAll">Get all child data</button>
  </div>
</template>

<script>
const test = {
  props: ['message', 'index'],
  template: '<div><h1>Reference {{ index }}</h1><input v-model="message.line" type="text"><br />Value from mode: <b>{{message.line}}</b></div>',
  watch: {
    'message.line': function (val) {
      console.log('changing', val, this.message)
    }
  }
}

export default {
  name: 'app',
  data () {
    return {
      messages: [{
        line: 'hello'
      }, {
        line: 'vue'
      }, {
        line: 'js'
      }]
    }
  },
  methods: {
    getAll: function (e) {
      let childrenMessage = ''
      this.$children.forEach((child) => {
        childrenMessage += child.message.line + ' '
      })
      console.log(childrenMessage)
      alert(childrenMessage)
    }
  },
  components: {
    'test': test
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
