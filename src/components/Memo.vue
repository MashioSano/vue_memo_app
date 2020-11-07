<template>
  <div>
    <MemoForm @createOrUpdate="createOrUpdate" @destroy="destroy" :id="currentMemoId" :memo="currentMemo"></MemoForm>
    <MemoList v-for="(memo, key) in firstLines()" :key="key" :id="key" v-bind:memo="memo" @currentMemo="current"></MemoList>
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
        currentMemoId: undefined,
        currentMemo: undefined
      }
    },
    methods: {
      firstLines(){
        return this.memos.map(element => (element.split(/\r\n|\r|\n/)[0]))
      },
      createOrUpdate(value, id){
        if(id===undefined){
          this.memos.push(value)
          localStorage.setItem('memos', JSON.stringify(this.memos))
        }else{
          this.memos[id] = value
          localStorage.setItem('memos', JSON.stringify(this.memos))
        }
      },
      destroy(id){
        console.log("aaa")
        this.memos.splice(id, 1)
        localStorage.setItem('memos', JSON.stringify(this.memos))
      },
      current(memo, id){
        console.log("Memo.vueのcurrentメソッド", memo, id)
        this.currentMemo = memo
        this.currentMemoId = id
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
