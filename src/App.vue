<template>
  <div id="app">
    <div class="noteList">
      <div class="addBtm"><b>+ Add note</b></div>
      <div class="notesListTi" v-for="(note, index) in notes" :key="index" @click="tap(index)">
        {{ note.title }}
      </div>
    </div>
    <editor :key="index" :current-note="currentNote" />
    <viewer :key="index" :preview-data="preNote" />
  </div>
</template>

<script src="https://unpkg.com/vue/dist/vue.js"></script>
<script src="https://unpkg.com/marked"></script>
<script>
import notes from "./components/notes";
import editor from "./components/editor";
import viewer from "./components/viewer";

export default {
  name: "App",
  props: {
    appData: {
      type: Object,
      required: true,
    },
  },
  components: {
    notes,
    editor,
    viewer,
  },
  data() {
    return {
      currentNote: {
        title: "000",
        favorite: false,
        content: "ZZZZZZZ",
        id: "0",
      },
      notes: [
        {
          title: "111",
          favorite: false,
          content: "oneoneone",
          id: "1",
        },
        {
          title: "222",
          favorite: false,
          content: "twotwotwo",
          id: "2",
        },
      ],
    };
  },
  methods: {
    tap(id) {
      this.currentNote = this.notes[id];
    }
  },
};
</script>

<style lang="scss">
body {
  margin: 0px;
}
#app {
  position: relative;
  display: flex;
  height: 100%;
  margin: 0px;

  .noteList {
    background-color: yellow;
    position: relative;
    height: 95vh;
    width: 20vw;
    box-sizing: border-box;

    .addBtm {
      position: relative;
      background-color: #3cbb84;
      color: white;
      width: 120px;
      font-size: 23px;
      padding: 5px;
      border-radius: 3px;
      margin: 5px;
      cursor: pointer;
      margin-bottom: 20px;
    }

    .notesListTi {
      cursor: pointer;
      height: 45px;
      display: flex;
      align-items: center;
      &:hover {
        background-color: plum;
      }
    }
  }
}
</style>
