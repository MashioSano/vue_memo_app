<template>
  <div>
    <MemoForm @createOrUpdate="createOrUpdate" @destroy="destroy" :memo="currentMemo"></MemoForm>
    <MemoList v-for="(memo, key) in memos" :key="key" :id="key" v-bind:memo="memo" @currentMemo="current"></MemoList>
  </div>
</template>

<script>
  import MemoForm from "../components/MemoForm.vue"
  import MemoList from "../components/MemoList.vue"

  export default {
    components: {
      MemoForm,
      MemoList
    },
     data(){
      return {
        memos: [],
        currentMemo: undefined
      }
    },
    methods: {
      firstLines(){
        return this.memos.map(element => (element.split(/\r\n|\r|\n/)[0]))
      },
      createOrUpdate(value, memo){
        if(memo===undefined){
          let newMemo = {id: this.$uuid.v4(), description: value}
          this.memos.push(newMemo)
          localStorage.setItem('memos', JSON.stringify(this.memos))
          this.currentMemo=undefined
        }else{
          const target = this.memos.find((m) => {
            return (m.id === memo.id)
          })
          target.description = value
          localStorage.setItem('memos', JSON.stringify(this.memos))
          this.currentMemo=undefined
        }
      },
      destroy(memo){
        if (memo){
          const index = this.memos.findIndex((v) => v.id === memo.id);
          this.memos.splice(index, 1)
          localStorage.setItem('memos', JSON.stringify(this.memos))
          this.currentMemo=undefined
        }
      },
      current(memo){
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
