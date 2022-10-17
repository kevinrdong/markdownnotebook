<template>
  <textarea name="" id="" cols="30" rows="10"></textarea>
</template>

<script>
export default {
  props: {
    noteData: {
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