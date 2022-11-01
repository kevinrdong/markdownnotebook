<template>
  <div id="app">
    <div class="noteList">
      <div class="addBtm" @click="addNote"><b>+ Add note</b></div>
      <div
        class="notesListTi"
        tabindex="-1"
        v-for="(note, index) in notes"
        :key="index"
        @click="tap(note.id)"
      >
        {{ note.title }}
        <div class="star" v-show="note.favorite">★</div>
      </div>
    </div>
    <editor
      :key="index"
      :current-note="currentNote"
      @favorite="setFavorite"
      @deleteIt="setDeleteIt"
    />
    <viewer :key="index" :preview-note="currentNote" />
  </div>
</template>

<script>
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
    editor,
    viewer,
  },
  data() {
    return {
      currentNote: {},
      sampleNote: {
        title: "000",
        favorite: false,
        content: `# title  
          ## title 
          **粗體** 
          *斜體*
          ***粗又斜***
          
          - ewd
          - ggg
          `,
        id: "0",
      },
      notes: [
        // {
        //     title: "",
        //     favorite: false,
        //     content:
        //     `# title
        //     ## title
        //     **粗體**
        //     *斜體*
        //     ***粗又斜***
        //     >引用段落
        //     >
        //     段落
        //     `,
        //     id: "0",
        //   },
        //   {
        //     title: "111",
        //     favorite: false,
        //     content:
        //       "Do consectetur adipisicing elit consectetur aliqua. Ullamco elit tempor commodo cillum cillum. Occaecat nostrud anim aliqua Lorem. Elit aliqua laborum esse adipisicing irure ex aliquip culpa nulla. Pariatur sit labore id quis ut elit tempor anim enim enim aliquip do proident. Do ex ipsum pariatur cupidatat labore deserunt non do amet deserunt ex excepteur culpa cupidatat. Tempor et amet do anim aute sint occaecat.Tempor nulla officia deserunt pariatur occaecat ipsum. Lorem eu adipisicing nostrud dolore irure consectetur Lorem mollit culpa duis Lorem duis laboris. Enim laborum ut mollit minim. Enim pariatur officia voluptate nostrud id enim enim ullamco elit. Quis eu occaecat eu ipsum aliqua sint. Non adipisicing culpa excepteur elit culpa dolor enim laboris sunt.",
        //     id: "1",
        //   },
        //   {
        //     title: "222",
        //     favorite: false,
        //     content:
        //       "Reprehenderit ea nisi id ullamco culpa est qui occaecat veniam laborum pariatur. Qui laborum non esse excepteur mollit id sit. Minim minim est eiusmod ut nulla aute sit id dolore. Duis nostrud officia amet velit. Culpa minim minim irure fugiat eiusmod esse sint quis cupidatat minim duis. Quis veniam dolor enim incididunt aute esse amet duis pariatur incididunt velit sit mollit deserunt. Commodo et esse nisi mollit ea velit ut.Ea deserunt minim commodo aliquip labore labore veniam sit laboris Lorem in nostrud labore. Aliquip pariatur aute minim Lorem eiusmod laborum dolore cillum magna. Adipisicing occaecat minim officia enim ad cillum ea. Tempor mollit ex ad amet et.",
        //     id: "2",
        //   },
        //   {
        //     title: "333",
        //     favorite: false,
        //     content:
        //       "Anim commodo ut excepteur fugiat anim ullamco veniam cupidatat adipisicing et ex. Ullamco pariatur nisi anim est sit proident velit. Reprehenderit aute incididunt ad velit incididunt esse consequat consequat do nulla duis excepteur irure commodo. Ipsum velit ut id sunt reprehenderit ad deserunt. Aute ex fugiat dolor excepteur culpa ex nisi laborum ut adipisicing ipsum fugiat officia exercitation.Consectetur sunt est quis Lorem. Ad voluptate quis commodo in labore eu nostrud minim consectetur consequat dolore cupidatat commodo dolor. Culpa aute ad nostrud amet excepteur occaecat pariatur proident nisi dolor dolor. Adipisicing et occaecat commodo quis nostrud cupidatat.",
        //     id: "3",
        //   },
      ],
    };
  },
  watch: {
    "currentNote.content": "saveNotes",
    "currentNote.title": "saveNotes",
    "currentNote.favorite": "saveNotes",
  },
  methods: {
    tap(id) {
      var index = this.notes.findIndex((note) => {
        return note.id === id;
      });
      console.log(index);
      // var newObject = this.notes[index];
      this.currentNote = this.notes[index];

      // this.currentNote = this.notes[id];
    },
    guideSample() {
      this.currentNote = this.sampleNote;
    },

    setFavorite(id) {
      // console.log("id",id)
      var index = this.notes.findIndex((note) => {
        return note.id === id;
      });
      // console.log("index",index)
      var newObject = this.notes[index];
      // console.log(newObject)
      newObject.favorite = !newObject.favorite;
      this.notes.splice(index, 1, newObject);
    },
    setDeleteIt(id) {
      localStorage.removeItem(`this.currentNote ${this.currentNote.id}`);
      var index = this.notes.findIndex((note) => {
        return note.id === id;
      });
      this.currentNote = this.notes[index + 1];
      this.notes.splice(index, 1);

      if (this.notes.length == 0) {
        this.guideSample();
      }
    },
    addNote() {
      var newNote = {
        title: "New Note",
        favorite: false,
        content: "",
        id: parseInt(this.currentNote.id + 1),
      };
      this.notes.push(newNote);
    },
    saveNotes() {
      console.log("123");
      var toSaveC = JSON.stringify(this.currentNote);
      // var toSaveI = JSON.stringify(this.currentNote.content)
      localStorage.setItem(`this.currentNote ${this.currentNote.id}`, toSaveC);
    },
  },
  created() {
    // var getDateC = localStorage.getItem(`this.currentNote ${ this.currentNote.id }`)
    if (localStorage.length !== 0) {
      // var getArrayC = JSON.parse(getDateC)
      var getData = Object.entries(localStorage);
      var arr = getData.filter((e) => {
        return (
          e[0].includes("this.currentNote") &&
          !e[0].includes("this.currentNote 0")
        );
      });
      var edit = arr
        .map((e) => {
          return JSON.parse(e[1]);
        })
        .sort((a, b) => {
          return a.id - b.id;
        });
      this.notes = edit;
    } else {
      this.guideSample();
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
    background-color: #e8f5e9;
    position: relative;
    min-height: 100vh;
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
      padding-left: 10px;
      justify-content: space-between;
      &:hover {
        background-color: #3cbb84;
      }
      &:focus {
        background-color: #3cbb84;
      }

      .star {
        position: relative;
        font-size: 25px;
        left: -10%;
      }
    }
  }
}
</style>
