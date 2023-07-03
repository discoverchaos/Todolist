<template>
  <Navbar 
  :lang="lang"
  @changeLang="changeLang"
  @find="search = $event" 
   />
  <Notes :search="search" :notes="filterNotes" @delNote="delNote" @changeNote="changeNote" :lang="lang"/>
  <Modal
    v-show="showModal"
    @showOrClose="showModal = false"
    @addNote="addNote"
    :edit="edit"
    :curNote="curNote"
    :currentId="currentId"
    @editedNote="editedNote"
    @editFalse="editFalse"
  />
  <AddButton @openModal="showModal = !showModal" />
</template>
<script>
import AddButton from "./components/AddButton.vue";
import Modal from "./components/Modal.vue";
import Navbar from "./components/Navbar.vue";
import Notes from "./components/Notes.vue";
// import { v4 as uuidv4 } from 'uuid';
import langs from './lang.js'

export default {
  components: { Navbar, Notes, Modal, AddButton },
  data() {
    return {
      notes: [],
      showModal: false,
      curNote: {},
      edit: false,
      currentId: localStorage.id ? localStorage.id : localStorage.id = 0,
      lang: 'ru',
      langWords: {},
      search: ''
    };
  },
  methods: {
    addNote(obj) {
      const note = { ...obj };
      note.date = new Date().toLocaleString();
      note.id = this.currentId++;
      this.notes.push(note);
    },
    delNote(id) {
      const idx = this.notes.findIndex((c) => c.id == id);
      this.notes.splice(idx, 1);
    },
    getNotes() {
      if (localStorage.notes) {
        this.notes = JSON.parse(localStorage.notes);
      }
    },
    changeNote(id) {
      this.edit = this.showModal = true;
      let pickedNote = this.notes.find((note) => note.id == id);
      this.curNote = pickedNote;
    },
    editedNote(noteEdited) {
      this.notes.forEach((note) => {
        if (note.id == noteEdited.id) {
          note.title = noteEdited.title;
          note.text = noteEdited.text;
          note.date = noteEdited.date;
        }
      });
      this.showModal = false;
      setTimeout(() => {
        this.edit = false;
      }, 500);
    },
    editFalse() {
      setTimeout(() => {
        this.edit = false;
        
      }, 500);
    },
    changeLang(val){
      this.lang = localStorage.lang = val
    }
  },
  created() {
    this.getNotes();
    localStorage.lang = localStorage.lang || 'ru'
    this.lang = localStorage.lang || 'ru'
    this.langWords = langs
    localStorage.words = JSON.stringify(this.langWords)
  },
  provide() {
    return {
        words: localStorage.words ? JSON.parse(localStorage.words) : location.reload()
    }
  },
  watch: {
    notes: {
      handler() {
        localStorage.notes = JSON.stringify(this.notes);
      },
      deep: true,
    },
  },
  computed: {
    filterNotes(){
      if(this.search){
        let se = this.search.toLowerCase()
        const filterNotes = this.notes.filter(item => {
          const title = item.title.toLowerCase()
          const text =  item.text.toLowerCase()
          if (title.includes(se)) return item
          if (text.includes(se)) return item
        })
        return filterNotes
      }
      else return this.notes
    }
  }
};
</script>
<style lang="scss">
</style>