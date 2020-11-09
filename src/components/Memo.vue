<template>
  <div class="main">
    <MemoForm @createOrUpdate="createOrUpdate" @destroy="destroy" :memo="currentMemo"></MemoForm>
    <div class="memos">
      <MemoDetail v-for="(memo, key) in memos" :key="key" :memo="memo" @clickedMemo="updateCurrentMemo"></MemoDetail>
    </div>
  </div>
</template>

<script>
import MemoForm from '../components/MemoForm.vue'
import MemoDetail from '../components/MemoDetail.vue'

export default {
  components: {
    MemoForm,
    MemoDetail
  },
  data () {
    return {
      memos: [],
      currentMemo: undefined
    }
  },
  methods: {
    firstLines () {
      return this.memos.map(element => (element.split(/\r\n|\r|\n/)[0]))
    },
    createOrUpdate (value, memo) {
      if (memo === undefined) {
        const newMemo = { id: this.$uuid.v4(), description: value }
        this.memos.push(newMemo)
        localStorage.setItem('memos', JSON.stringify(this.memos))
        this.currentMemo = undefined
      } else {
        const target = this.memos.find((m) => {
          return (m.id === memo.id)
        })
        target.description = value
        localStorage.setItem('memos', JSON.stringify(this.memos))
        this.currentMemo = undefined
      }
    },
    destroy (memo) {
      if (memo) {
        const index = this.memos.findIndex((v) => v.id === memo.id)
        this.memos.splice(index, 1)
        localStorage.setItem('memos', JSON.stringify(this.memos))
        this.currentMemo = undefined
      }
    },
    updateCurrentMemo (memo) {
      this.currentMemo = memo
    }
  },
  mounted () {
    if (localStorage.getItem('memos')) {
      try {
        this.memos = JSON.parse(localStorage.getItem('memos'))
      } catch (e) {
        localStorage.removeItem('memos')
      }
    }
  }
}
</script>

<style scoped>
  .main{
    max-width: 600px;
    margin: 0 auto;
    background-color: #42b983;
    display: flex;
    flex-direction: row;
    justify-content: center;
  }
  .memos{
    margin: 3px;
  }
</style>
