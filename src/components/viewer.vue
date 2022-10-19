<template>
  <div class="viewNote">
    <textarea name="viewer"  readonly="readonly" class="viewNotes" v-model="previewNote.content" />
  </div>
</template>
  
  <script>


export default {
  props: {
    previewNote: {
      type: Object,
      required: true,
    },
   
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
  .viewNotes {
    background-color: green;
    height: 95vh;
    width: 40vw;
  }
}
</style>