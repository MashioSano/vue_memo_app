<template>
  <div>
    <h1>フォーム</h1>
    <button @click="formup">+</button>
     <form v-if="formDisplay">
        <textarea v-model="value"></textarea>
        <input type="button" value="編集" v-on:click="aaa">
        <input type="button" value="削除" v-on:click="toDelete">
     </form>
  </div>
</template>

<script>
export default {
  props: {
    memo: Object,
  },
  data(){
    return {
      formDisplay: false,
      value: "新規メモ"
    }
  },
  methods: {
    formup(){
      this.formDisplay=true
    },
    aaa(){
      this.$emit("createOrUpdate", this.value, this.memo)
      this.formdown()
    },
    toDelete(){
      this.$emit("destroy", this.memo)
      this.formdown()
    },
    formdown(){
      this.formDisplay=false
    }
  },
  watch: {
    memo(newMemo){
      this.formup()
      this.value=newMemo.description
    }
  }
}
</script>
