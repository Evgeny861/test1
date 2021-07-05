<template>
    <div class="new-note">
        <label>Заголовок</label>
        <input type="text" v-model="note.title">
        <label>Описание</label>
        <textarea v-model="note.description"></textarea>
        <button class="btn btnPrimary" @click="addNote">Добавить заметку</button>
    </div>
</template>

<script>
export default {
    props: {
        note: {
            type: Object,
            required: true
        }
    },

    methods: {
        addNote() {
            this.$emit('addNote', this.note)
        }
    }
}
</script>

<style>

    .new-note {
        text-align: center;
    }
    .btn {
        display: inline-block;
        padding: .8em 2.6em;
        margin: 20px 0;
        line-height: 1;
        text-transform: uppercase;
        cursor: pointer;
        border-radius: 30px;
    }

    .btnPrimary {
    color: #ffffff;
    border: 1px solid #494ce8;
    background-color: #494ce8;
  }
</style>