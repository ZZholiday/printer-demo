<template>
  <div v-bind:style="{ display: 'flex', width: type===0?150:300 + 'px' }">
    <div v-bind:style="{ display: 'flex', width: prefixWidth + 'px' }">
      <span>
        <b>{{prefix}}</b>
      </span>
    </div>
    <div v-bind:style="{'text-align':'center', width: (width-prefixWidth) + 'px' }">{{content}}</div>
  </div>
</template>

<script>
export default {
  name: "PrintCell",
  props: {
    width: {
      type: Number,
      default: 150
    },
    prefixWidth: {
      type: Number,
      default: 50
    },
    type: {
      type: Number,
      default: 0
    },
    prefix: {
      type: String,
      default: ""
    },
    content: {
      type: String,
      default: ""
    }
  },
  methods: {},
  mounted() {}
};
</script>

<style scoped>
</style>
