<template>
  <div class="viewNote">
    <vue-marked>{{previewNote.content}}</vue-marked>  </div>
</template>
  
<script>
import VueMarked from 'vue-marked';
export default {
  props: {
    previewNote: {
      type: Object,
      required: true,
    },
   
  },
  components: {
    VueMarked,
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
  padding: 15px;
    box-sizing: border-box;
    // background-color: green;
    height: 95vh;
    width: 40vw;

}
</style>