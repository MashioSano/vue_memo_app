<template>
  <div>
    <button @click="formup" class="button">+</button>
     <form v-if="formDisplay">
        <textarea v-model="value" rows="8" cols="40"></textarea>
        <div>
          <input type="button" value="編集" v-on:click="emitMemo('createOrUpdate')" class="button">
          <input type="button" value="削除" v-on:click="emitMemo('destroy')" class="button">
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
    }
  },
  methods: {
    emitMemo (action) {
      if (action === 'destroy'){
        this.$emit('destroy', this.memo)
        this.formdown()
      } else {
        this.$emit('createOrUpdate', this.value, this.memo)
        this.formdown()
      }
    },
    formup () {
      this.formDisplay = true
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
