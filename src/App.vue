<template>
  <div id="app">
    <div class="wrapper">
      <div class="wrapper-content">
        <section>
          <div class="container">
            <message v-if="message" :message="message"></message>

            <newNote :note="note" @addNote="addNote"></newNote>

            <div class="note-header">
              <h1>{{ title }}</h1>
              <search
                :value="search"
                @search="search = $event"
                placeholder="Найти заметку"
              ></search>
              <div class="icons">
                <svg
                  :class="{ active: grid }"
                  @click="grid = true"
                  style="cursor: pointer;"
                  xmlns="http://www.w3.org/2000/svg"
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <rect x="3" y="3" width="7" height="7"></rect>
                  <rect x="14" y="3" width="7" height="7"></rect>
                  <rect x="14" y="14" width="7" height="7"></rect>
                  <rect x="3" y="14" width="7" height="7"></rect>
                </svg>
                <svg
                  :class="{ active: !grid }"
                  @click="grid = false"
                  style="cursor: pointer;"
                  xmlns="http://www.w3.org/2000/svg"
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <line x1="8" y1="6" x2="21" y2="6"></line>
                  <line x1="8" y1="12" x2="21" y2="12"></line>
                  <line x1="8" y1="18" x2="21" y2="18"></line>
                  <line x1="3" y1="6" x2="3" y2="6"></line>
                  <line x1="3" y1="12" x2="3" y2="12"></line>
                  <line x1="3" y1="18" x2="3" y2="18"></line>
                </svg>
              </div>
            </div>

            <notes
              :notes="notesFilter"
              :grid="grid"
              @remove="removeNote"
            ></notes>
          </div>
        </section>
      </div>
    </div>
  </div>
</template>

<script>
import message from "./components/Message.vue";
import newNote from "./components/NewNote.vue";
import notes from "./components/Notes.vue";
import search from "./components/Search.vue";

export default {
  components: {
    message,
    notes,
    newNote,
    search,
  },
  name: "App",

  data() {
    return {
      title: "Notes App",
      search: "",
      message: null,
      grid: true,
      note: {
        title: "",
        description: "",
      },
      notes: [
        {
          title: "First Note",
          description: "Описание первой заметки",
          date: new Date(Date.now()).toLocaleDateString(),
          id: 1,
          isEdit: false
        },
        {
          title: "Second Note",
          description: "Описание второй заметки",
          date: new Date(Date.now()).toLocaleDateString(),
          id: 2,
          isEdit: false
        },
        {
          title: "Third Note",
          description: "Описание третьей заметки",
          date: new Date(Date.now()).toLocaleDateString(),
          id: 3,
          isEdit: false
        },
      ],
    };
  },

  computed: {
    notesFilter() {
      let array = this.notes,
        search = this.search;

      if (!search) return array;

      search = search.trim().toLowerCase();

      array = array.filter(function(item) {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item;
        }
      });
      return array;
    },
  },

  methods: {
    addNote() {
      let { title, description } = this.note;

      if (title === "") {
        this.message = "Заголовок не может быть пустым!";
        return false;
      }

      this.notes.push({
        title,
        description,
        date: new Date(Date.now()).toLocaleDateString(),
        id: new Date().getTime(),
        isEdit: false
      });

      this.message = null;
      this.note.title = "";
      this.note.description = "";
    },

    removeNote(index) {
      this.notes.splice(index, 1);
    },
  },
};
</script>

<style>
html {
  line-height: 1.4;
  font-size: 18px;
  color: #101010;
  height: 100%;
  @media screen and (max-width: $desktopWidth) {
    font-size: 16px;
  }
  @media screen and (max-width: $tableWidth) {
    font-size: 15px;
  }
  @media screen and (max-width: $phoneWidth) {
    font-size: 14px;
  }
}

body {
  font-family: "Montserrat", Helvetica, Arial, sans-serif;
  font-size: 18px;
  font-weight: 400;
  margin: 0;
  padding: 0;
  background-color: #f7f7f7;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  margin: 0;
}

input,
textarea,
select,
button {
  border: 1px solid #dcdfe6;
}

a {
  text-decoration: none;
}

ul,
li {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

.wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  margin: 0 auto;
}

.content-wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.container {
  width: 100%;
  flex: 0 0 auto;
  position: relative;
  max-width: 1280px;
  margin: 0 auto;
  padding: 30px 0 0 0;
  @media screen and (max-width: 980px;) {
    max-width: 768px;
  }
  @media screen and (max-width: 768px;) {
    max-width: 480px;
  }
  @media screen and (max-width: 480px;) {
    max-width: 320px;
  }
}

/* controls */

label {
  display: block;
  font-size: 16px;
  margin-bottom: 10px;
  text-align: center;
}
input {
  padding: 16px 26px;
  margin-bottom: 30px;
  border-radius: 20px;
}
textarea {
  padding: 30px 27px;
  border-radius: 14px;
}
input,
textarea {
  width: 90%;
}

.note-header {
  margin: 36px 0;
}
</style>
