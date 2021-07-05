<template>
<div class="notes">
    <div class="note" :class="{ full: !grid }"  v-for="(note, index) in notesList" :key="note.id">
        <div class="note-header" :class="{ full: !grid }">
            <p :contenteditable="note.isEdit" @input="input($event, note)" :key="note.isEdit">{{ note.title }}</p>
            <p style="cursor: pointer;" @click="removeNote(index)">X</p>
        </div>
        <div class="note-body">
            <p >{{ note.description }}</p>
            <div class="last-str">

            <span>{{ note.date }}</span>
            <span v-if="!note.isEdit"  @click="edit(note)">Edit</span>
            <span v-else @click="save(note)">Save</span>
            </div>
        </div>
    </div>
</div>
</template>

<script>
export default {
    props: {
        notes: {
            type: Array,
            required: true
        },
        grid: {
            type: Boolean,
            required: true
        }
    },
    data(){
        return {
            notesList: [],
        }
    },
    mounted(){
        this.notesList = this.notes
    },
    methods: {
        input(e, note) {
            this.notesList.find(el => el.id === note.id).title = e.target.textContent
        },
        edit(note){
            this.notesList.find(el => el.id === note.id).isEdit = true
        },
        save(note){
            this.notesList.find(el => el.id === note.id).isEdit = false
        },
        removeNote(index) {
            this.$emit('remove', index);
        }
    }
}
</script>

<style>
.last-str {
    display: flex;
    justify-content: space-between;
    cursor: pointer;
}
    .notes {
        display: flex;
        align-items: center;
        justify-content: space-between;
        flex-wrap: wrap;
        padding: 40px 0;
    }

    .note {
        width: 28%;
        padding: 10px 20px;
        margin: 0 20px 32px 0;
        background-color: #fff;
        transition: all .25s cubic-bezier(.02,.01,.47,1);
        box-shadow: 0 30px 30px rgba(0,0,0,.02);
    }

    .note:hover {
        box-shadow: 0 30px 30px rgba(0,0,0,.04);
        transform: translate(0,-6px);
        transition-delay: 0s !important;
    }

    .note.full {
        width: 100%;
        text-align: center;
    }

    .note-header {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .note-header.full {
        justify-content: center;
        margin-bottom: 10px;
    }

    .note-header.full p {
        margin: 0 16px 0 0;
    }

    .note-header h1 {
        font-size: 32px;
    }

    .note-header p {
        font-size: 22px;
        color: #402caf;
    }

    .note-header svg {
        margin-right: 12px;
        color: #999;
    }

    .note-header svg.active {
        color: #402caf;
    }

    .note-header svg:last-child {
        margin-right: 0px;
    }

    .note-body p {
        margin: 20px 0;
    }

    .note-body span {
        font-size: 14px;
        color: #999;
    }
</style>