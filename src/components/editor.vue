<template>
  <div class="currentNote">
    <div class="title">
      <input type="text" class="typeTitle"  v-model="currentNote.title" />
      <div class="bt" @click="favorite">☆</div>
      <div class="bt">🗑︎</div>
    </div>
    <textarea name="edit" class="edit" v-model="currentNote.content" />
  </div>
</template>
  
  <script>

export default {
  props: {
    currentNote: {
      type: Object,
      required: true,
    }
  },
  data() {
    return {
      
    };
  },
  methods: {
    favorite() {
      this.$emit('favorite',this.currentNote.id)
    }
  },
};
</script>

<style lang="scss">
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
      background-color: #3cbb84;
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
    max-width: 39vw;
    height: 86vh;
    padding: 10px;
  }
}
</style>