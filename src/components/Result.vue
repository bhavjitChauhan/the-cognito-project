<template>
  <div>
    <h2>{{ this.result.source }}</h2>
    <p>{{ this.result.data }}</p>
  </div>
</template>

<script>
export default {
  name: "Result",
  props: {
      result: Object
  }
};
</script>

<style scoped>
    div {
        border-style: solid
    }
</style>
