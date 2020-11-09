<template>
  <div>
    <a href="#" v-on:click="current">{{ firstLine }}</a>
  </div>
</template>

<script>
export default {
  props: {
    memo: Object
  },
  methods: {
    current () {
      this.$emit('clickedMemo', this.memo)
    }
  },
  computed: {
    firstLine: function () {
      return this.memo.description.split(/\r\n|\r|\n/)[0]
    }
  }
}
</script>

<style scoped>
  a{
    color:black;
  }
</style>
