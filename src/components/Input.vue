<template>
  <input type="text" v-model="value" @keypress.enter.prevent="keypress" @blur="blur">
</template>

<script>
export default {
  name: "Input",
  props: {
    parent: {
      type: Element,
      require: true
    },
    text: {
      type: String,
      require: true
    }
  },
  data: function() {
    return {
      value: this.text
    };
  },
  mounted: function() {
    this.parent.appendChild(this.$el);
    this.$nextTick(() => {
      this.$el.focus();
    });
  },
  methods: {
    keypress: function() {
      this.$emit("change", this.value);
      this.$destroy();
    },
    blur: function() {
      this.$destroy();
    }
  },
  destroyed: function() {
    this.$el.remove();
  }
};
</script>

<style scoped>
input[type="text"] {
  display: inline-block;
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  border-radius: 1px;
  border: 1px solid #333;
  padding: 0;
  height: 100%;
}
</style>
