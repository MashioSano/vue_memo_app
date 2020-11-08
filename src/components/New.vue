<template>
  <div>
    <button @click="formup(newMemo)">+</button>
     <form v-show="pushed">
        <textarea v-model="newMemo"></textarea>
        <input type="button" v-on:click="updateOrCreate" value="編集">
        <input type="button" v-on:click="destroy" value="削除">
     </form>
        <div v-for="(memo, key) in firstLines()" :key="key" :id="key">
          <div class="memo">
            <a href="#" v-on:click="edit(memos[key], key)" class="discription">{{ memo }}</a>
          </div>
        </div>
  </div>
</template>

<script>
export default {
   data(){
      return {
        pushed: false,
        newMemo: "新規メモ",
        memos: [],
        id: undefined
      }
    },
    methods: {
      edit(memo, key){
        this.id=key
        this.newMemo = memo
        this.formup()
      },
      formup(){
        this.pushed=true
      },
      formdown(){
        this.pushed=false
        this.id=undefined
        this.newMemo = "新規メモ"
      },
      updateOrCreate(){
        if (this.id===undefined){
          this.memos.push(this.newMemo)
          localStorage.setItem('memos', JSON.stringify(this.memos))
          this.formdown()
        }else{
          this.memos[this.id] = this.newMemo
          localStorage.setItem('memos', JSON.stringify(this.memos))
          this.formdown()
        }
      },
      destroy(){
        this.memos.splice(this.id, 1)
        localStorage.setItem('memos', JSON.stringify(this.memos))
        this.formdown()
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
