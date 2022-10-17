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
}
</style>
