<template>
  <div class="hello">
    <div class="labels">
      <div @click="onClick" v-for="(label, index) in labels" :key="index">{{ label }}</div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import Input from '@/components/Input.vue'

const InputConstructor = Vue.extend(Input)

export default {
  name: 'HelloWorld',
  data: function () {
    return {
      input: null,
      labels: ['label1', 'label2', 'label3']
    }
  },
  methods: {
    onClick(e) {
      this.input = new InputConstructor({
        propsData: {
          parent: e.target,
          text: e.target.textContent
        }
      })
      this.input.$on('change', this.edited)
      this.input.$mount()
    },
    edited(e) {
      this.input.$el.parentElement.textContent = e
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

a {
  color: #42b983;
}

.labels > div {
  position: relative;
  text-align: left;
}
</style>
