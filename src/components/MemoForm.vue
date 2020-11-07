<template>
  <div>
    <h1>フォーム</h1>
    <button @click="formup">+</button>
     <form v-show="formDisplay">
        <textarea v-model="value"></textarea>
        <input type="button" value="編集" v-on:click="aaa">
        <input type="button" value="削除" v-on:click="toDelete">
     </form>
  </div>
</template>

<script>
export default {
  props: {
      memo: String,
      id: Number
  },
  data(){
    return {
      formDisplay: false,
      value: this.memo || "新規メモ"
    }
  },
  methods: {
    formup(){
      this.formDisplay=true
    },
    aaa(){
      console.log(this.memo, this.id)
      this.$emit("createOrUpdate", this.value, this.id)
      this.formdown()
    },
    toDelete(){
      this.$emit("destroy", this.id)
      this.formdown()
    },
    formdown(){
      this.formDisplay=false
    }
  },
  watch: {
    memo(newMemo){
      this.formup()
      this.value=newMemo
    }
  }
}
</script>
