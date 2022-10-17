<template>
  <div id="app">
    <div class="noteList">
      <div class="addBtm"><b>+ Add note</b></div>
      <div class="notes"></div>
    </div>
    <editor :key="index" :curr-data="currdate" />
    <viewer :key="index" :preview-data="predata" />
  </div>
</template>

<script src="https://unpkg.com/vue/dist/vue.js"></script>
<script src="https://unpkg.com/marked"></script>
<script>
import notes from "./components/notes";
import editor from "./components/editor";
import viewer from "./components/viewer";

export default {
  name: 'App',
  components: {
    notes,
    editor,
    viewer,
  },
  data() {
    return {
      notesDate: ["1","2",3],

    }
  },
}
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
      position: absolute;
      background-color: #3CBB84;
      color: white;
      padding: 5px;
      border-radius: 3px;
      margin: 5px;
      cursor: pointer;
    }
  }  
  .currentNote {
    background-color: blue;
    height: 95vh;
    width: 40vw;

    .title {
      position: relative;
      display: flex;
      margin: 5px;
      align-items: center;

      .typeTitle {
        height: 30px;
        width: 35%;
      }
      .bt {
        background-color: #3CBB84;
        color: white;
        padding: 5px;
        border-radius: 3px;
        margin: 5px;
        cursor: pointer;
        width: 30px;
        height: 30px;
        font-size: 23px;
        text-align: center;
        margin-left: 10px;
      }
    }
    .edit {
      background-color: pink;
      width: 39vw;
      height: 88vh;
      }
  }
  .viewNote {
    background-color: green;
    height: 95vh;
    width: 40vw;
  }
}
</style>
