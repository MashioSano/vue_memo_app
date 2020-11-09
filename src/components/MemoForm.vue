<template>
  <div>
    <button @click="formup" class="button">+</button>
     <form v-if="formDisplay">
        <textarea v-model="value" rows="8" cols="40"></textarea>
        <div>
          <input type="button" value="編集" v-on:click="toCreateOrUpdate" class="button">
          <input type="button" value="削除" v-on:click="toDelete" class="button">
        </div>
     </form>
  </div>
</template>

<script>
export default {
  props: {
    memo: Object
  },
  data () {
    return {
      formDisplay: false,
      value: '新規メモ',
      height: 100
    }
  },
  methods: {
    formup () {
      this.formDisplay = true
    },
    toCreateOrUpdate () {
      this.$emit('createOrUpdate', this.value, this.memo)
      this.formdown()
    },
    toDelete () {
      this.$emit('destroy', this.memo)
      this.formdown()
    },
    formdown () {
      this.formDisplay = false
      this.value = '新規メモ'
    }
  },
  watch: {
    memo (newMemo) {
      if (newMemo) {
        this.value = newMemo.description
        this.formup()
      }
    }
  }
}
</script>

<style scoped>
  .button{
    margin: 3px;
  }
</style>
