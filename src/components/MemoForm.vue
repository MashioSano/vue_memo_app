<template>
  <div>
    <button @click="show" class="button">+</button>
     <form v-if="display">
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
      display: false,
      value: '新規メモ',
    }
  },
  methods: {
    emitMemo (action) {
      if (action === 'destroy'){
        this.$emit('destroy', this.memo)
        this.hide()
      } else {
        this.$emit('createOrUpdate', this.value, this.memo)
        this.hide()
      }
    },
    show () {
      this.display = true
    },
    hide () {
      this.display = false
      this.value = '新規メモ'
    }
  },
  watch: {
    memo (newMemo) {
      if (newMemo) {
        this.value = newMemo.description
        this.show()
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
