<template>
  <div>
    <a href="#" v-on:click="current">{{ memo.description }}</a>
  </div>
</template>

<script>
export default {
  props: {
      memo: Object,
    },
  methods: {
    current(){
      this.$emit("currentMemo", this.memo)
    }
  }
}
</script>
