<template>
   <div class="viewNote">
      <div class="viewNotes" v-for="(note,index) in notesDate" :key="index">
        <notes :key="index" :note-data="note" />
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
        previewData: {
        type: Object,
        required: true,
      }
    },
    data() {
      return {
          ifStar: false,
      };
    },
  };
  </script>

<style lang="scss">
.viewNote {
    background-color: green;
    height: 95vh;
    width: 40vw;
  }
</style>