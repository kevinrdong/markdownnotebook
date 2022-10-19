<template>
  <div id="app">
    <div class="noteList">
      <div class="addBtm"><b>+ Add note</b></div>
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
    <editor :key="index" :current-note="currentNote" @favorite="setFavorite" />
    <viewer :key="index" :preview-note="currentNote" />
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
        content:
          "Ullamco voluptate eiusmod cupidatat incididunt voluptate laboris duis qui exercitation Lorem aliquip. Nulla consequat ex excepteur cillum labore incididunt. Amet voluptate consectetur elit veniam ex dolor aliqua Lorem incididunt dolore minim. Excepteur consequat proident reprehenderit consequat amet sint et nisi commodo nostrud do aliqua cupidatat.Exercitation amet eiusmod sint consectetur anim. In minim occaecat sint voluptate officia cillum exercitation ullamco ex. Nostrud est enim amet incididunt consequat non ex. Sint nulla ea occaecat velit reprehenderit excepteur veniam deserunt minim minim ad incididunt.",
        id: "0",
      },
      notes: [
        {
          title: "111",
          favorite: false,
          content:
            "Do consectetur adipisicing elit consectetur aliqua. Ullamco elit tempor commodo cillum cillum. Occaecat nostrud anim aliqua Lorem. Elit aliqua laborum esse adipisicing irure ex aliquip culpa nulla. Pariatur sit labore id quis ut elit tempor anim enim enim aliquip do proident. Do ex ipsum pariatur cupidatat labore deserunt non do amet deserunt ex excepteur culpa cupidatat. Tempor et amet do anim aute sint occaecat.Tempor nulla officia deserunt pariatur occaecat ipsum. Lorem eu adipisicing nostrud dolore irure consectetur Lorem mollit culpa duis Lorem duis laboris. Enim laborum ut mollit minim. Enim pariatur officia voluptate nostrud id enim enim ullamco elit. Quis eu occaecat eu ipsum aliqua sint. Non adipisicing culpa excepteur elit culpa dolor enim laboris sunt.",
          id: "1",
        },
        {
          title: "222",
          favorite: false,
          content:
            "Reprehenderit ea nisi id ullamco culpa est qui occaecat veniam laborum pariatur. Qui laborum non esse excepteur mollit id sit. Minim minim est eiusmod ut nulla aute sit id dolore. Duis nostrud officia amet velit. Culpa minim minim irure fugiat eiusmod esse sint quis cupidatat minim duis. Quis veniam dolor enim incididunt aute esse amet duis pariatur incididunt velit sit mollit deserunt. Commodo et esse nisi mollit ea velit ut.Ea deserunt minim commodo aliquip labore labore veniam sit laboris Lorem in nostrud labore. Aliquip pariatur aute minim Lorem eiusmod laborum dolore cillum magna. Adipisicing occaecat minim officia enim ad cillum ea. Tempor mollit ex ad amet et.",
          id: "2",
        },
        {
          title: "333",
          favorite: false,
          content:
            "Anim commodo ut excepteur fugiat anim ullamco veniam cupidatat adipisicing et ex. Ullamco pariatur nisi anim est sit proident velit. Reprehenderit aute incididunt ad velit incididunt esse consequat consequat do nulla duis excepteur irure commodo. Ipsum velit ut id sunt reprehenderit ad deserunt. Aute ex fugiat dolor excepteur culpa ex nisi laborum ut adipisicing ipsum fugiat officia exercitation.Consectetur sunt est quis Lorem. Ad voluptate quis commodo in labore eu nostrud minim consectetur consequat dolore cupidatat commodo dolor. Culpa aute ad nostrud amet excepteur occaecat pariatur proident nisi dolor dolor. Adipisicing et occaecat commodo quis nostrud cupidatat.",
          id: "3",
        },
        {
          title: "000",
          favorite: false,
          content:
            "Ullamco voluptate eiusmod cupidatat incididunt voluptate laboris duis qui exercitation Lorem aliquip. Nulla consequat ex excepteur cillum labore incididunt. Amet voluptate consectetur elit veniam ex dolor aliqua Lorem incididunt dolore minim. Excepteur consequat proident reprehenderit consequat amet sint et nisi commodo nostrud do aliqua cupidatat.Exercitation amet eiusmod sint consectetur anim. In minim occaecat sint voluptate officia cillum exercitation ullamco ex. Nostrud est enim amet incididunt consequat non ex. Sint nulla ea occaecat velit reprehenderit excepteur veniam deserunt minim minim ad incididunt.",
          id: "0",
        },
      ],
    };
  },
  methods: {
    tap(id) {
      var index = this.notes.findIndex((note) => {
        return note.id === id     
      })
      console.log(index)
      // var newObject = this.notes[index]; 
      this.currentNote = this.notes[index]; 

      // this.currentNote = this.notes[id]; 
    },
    setFavorite(id) {
      // console.log("id",id)
      var index = this.notes.findIndex((note) => {
        return note.id === id     
      })
      // console.log("index",index)
      var newObject = this.notes[index];
      // console.log(newObject)
      newObject.favorite = !newObject.favorite;
      this.notes.splice(index, 1, newObject)
    },
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
      padding-left: 10px;
      // justify-content: space-between;
      &:hover {
        background-color: #3cbb84;
      }
      &:focus {
        background-color: #3cbb84;
      }

      .star {
        position: relative;
        font-size: 25px;
        left: 80%;
      }
    }
  }
}
</style>
