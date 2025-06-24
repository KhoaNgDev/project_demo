<template>
  <div v-for="(tag, index) in tags" :key="index">{{ index + " : " + tag }}</div>
  <input type="text" :value="newTag" />
</template>

<script>
export default {
  data: () => ({
    tags: ["vue", "react", "angular"],
    newTag: "preact",
  }),
};
</script>
