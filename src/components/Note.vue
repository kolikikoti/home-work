<script>


export default {
  name: 'Note',
  props: {
    note: Object
  },
  emits: ['changeNote', 'deleteNote'], 
  methods: {
    editNote() {
      this.$emit('changeNote', this.note)
    },
    deleteNote() {
      this.$emit('deleteNote', this.note) 
    }
  }
}
</script>

<template>
    <div class="card">
        <p class="text">{{ note.text }}</p>
        <button @click="editNote">Изменить</button>
        <button>Удалить</button>
    </div>
</template>

<style>
    .card {
        width: 45%;
        border: 1px solid black;
        border-radius: 5px;
        background-color: aliceblue;
        margin: 10px 10px;
        padding: 5px;
        box-sizing: border-box;
    }

    .card .text {
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

</style>




