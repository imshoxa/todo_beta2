<template>
  <Navbar
  @searchValue="search = $event"
  :lang="lang"
  @changeLang="changeLang"
  />
  <Notes 
  :notes="filterNotes"
  @delNote="delNote"
  @changeNote="changeNote" 
  :search="search"
  :lang="lang"
  />
  <Model 
  @addNote="addNote"
  v-show="modelOpen" 
  @closeModel="closeModel" 
  :currentId="currentId"
  :edit="edit"
  :editNote="editNote"
  @editedNote="editedNote"
  />
  <AddButton @openModel="openModel"/>
</template>

<script>

import langs from '@/lang';
import Navbar from '@/components/Navbar.vue';
import Notes from '@/components/Notes.vue';
import Model from '@/components/Model.vue';
import AddButton from '@/components/AddButton.vue';
export default {
    components: {
      Navbar,
      Notes,
      Model,
      AddButton
    },
    data(){
      return{
        edit: false,
        currentId: 1,
        modelOpen: false,
        notes: [],
        editNote: {},
        search: '',
        lang: 'en',
        langwords: {}
      }
    },
    created(){
      this.getNotes();
      localStorage.lang = localStorage.lang || 'en'
      this.lang = localStorage.lang || 'en'
      this.langwords = langs
      localStorage.words = JSON.stringify(this.langwords)
    },
    computed:{
      filterNotes(){
        return this.search ? this.notes.filter(note => note.title.toLowerCase().includes(this.search.toLowerCase())) : this.notes
      }
    },
    // provide(){
    //   return{
    //     words: JSON.parse(localStorage.words)
    //   }
    // },
    methods:{
      openModel(){
        this.modelOpen = true
      },
      closeModel(status){
      this.modelOpen = status,
      // this.edit = false
      setTimeout(() => this.edit = false, 500)
      },
      addNote(item){
        this.notes.push(item),
        this.modelOpen = false
      },
      delNote(id){
        let index = this.notes.findIndex(note => note.id == id)
        this.notes.splice(index, 1)
      },
      getNotes(){
        const localNotes = localStorage.notes
        if(localNotes){
          this.notes = JSON.parse(localNotes)
        }
      },
      changeNote(id){
        this.edit = this.modelOpen = true
        const pickedNote = this.notes.find(note => note.id == id)
        this.editNote = pickedNote
      },
      editedNote(editNotes){
        this.notes.forEach(note => {
          if(note.id == editNotes.id){
            note.title = editNotes.title,
            note.descr = editNotes.descr,
            note.date = editNotes.date
          }
        })
      },
      changeLang(val){
        this.lang = localStorage.lang = val
      }
    },
    watch: {
      notes:{
        handler(newNotes){
        localStorage.notes = JSON.stringify(this.notes)
      },
      deep: true
      }
    }
}
</script>

<style>

</style>
