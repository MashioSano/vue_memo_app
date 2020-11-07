<template>
  <div>
    <a href="#" v-on:click="current">{{ memo }}</a>
  </div>
</template>

<script>
export default {
  props: {
      memo: String,
      id: Number
    },
  methods: {
    current(){
      this.$emit("currentMemo", this.memo, this.id)
    }
  }
}
</script>
