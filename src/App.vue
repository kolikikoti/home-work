<template>
  <div class="app">
    <div class="notes">
      <Note 
        v-for="note in notes" 
        :key="note.id" 
        :note="note" 
        @changeNote="editNote" 
        
      />
    </div>
    <div class="writeBlock">
      <input type="text" placeholder="Поиск...">
      <textarea v-model="newNote" rows="10" cols="30" placeholder="Текст вашей заметки..."></textarea>
      <button v-if="!isEdit" @click="addNote">Добавить</button>
      <button v-else @click="saveNote(newId, newNote)">Сохранить</button>
    </div>
  </div>
</template>

<script>
import Note from './components/Note.vue';

export default {
  name: 'App',
  components: {
    Note,
  },
  methods: {
    addNote() {
      this.notes.unshift({
        id: Date.now(),
        text: this.newNote,
      });
    },
    editNote(note) {
      this.isEdit = true;
      this.newNote = note.text;
      this.newId = note.id;
    },
    saveNote(id, newText) {
      this.notes = this.notes.map((note) => {
        if (note.id == id) {
          note.text = newText;
        }
        return note;
      });
      this.isEdit = false;
      this.newNote = '';
    },
    deleteNote(note) {
      this.notes = this.notes.filter((n) => n.id !== note.id);
    },
  },
  data() {
    return {
      newNote: '',
      newId: '',
      isEdit: false,
      notes: [
        { id: 1, text: 'Пиривет'  },
        { id: 2, text: 'Lorem Ipsum' },
        { id: 3, text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Recusandae illo reiciendis aliquam ipsam similique, cum delectus iusto nulla officiis ullam sit assumenda' },
        { id: 4, text: 'Моя заметка номер 4' },
        { id: 5, text: 'Моя заметка номер 5' },
        { id: 6, text: 'Моя заметка номер 6' },
        { id: 7, text: 'Моя заметка номер 7' },
        { id: 8, text: 'Моя заметка номер 8' },
        { id: 9, text: 'Моя заметка номер 9' },
      ]
    };
  },
};


</script>

<style>
.app {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  width: 100%;

}

.notes {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  width: 50%;
}

.writeBlock {
  display: flex;
  flex-direction: column;
  align-items: center;

  width: 50%;
}

.writeBlock textarea {
  width: 300px;
  height: 300px;
  resize: none;
  margin: 5px 0;
}

.writeBlock button {
  width: 300px;
}
</style>
