<template>
  <div>
    <a href="#" v-on:click="current">{{ fistLine }}</a>
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
  },
  computed: {
    fistLine: function(){
       return this.memo.description.split(/\r\n|\r|\n/)[0]
    }
  }
}
</script>
