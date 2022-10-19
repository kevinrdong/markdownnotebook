<template>
  <div>notenotenotenotenotenotenotenote</div>
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