<script>

export default {
  data: () => ({
    jsFrameworks: ["react.js", "vue.js", "angular"],
    backendFrameworks: [],
  }),
  //mounted() là lifecycle hook trong Vue.
  //Hàm này sẽ chạy sau khi component được gắn vào DOM (mounted).
  methods: {
    handleChange(tags) {
      this.jsFrameworks = [...tags];
    },
  },
};
</script>

<template>
<h1>Your favorite frameworks</h1>
  <div>{{ jsFrameworks }}</div>
  <tags-input :selected-tags="jsFrameworks" @change="handleChange" />

  <div>{{ backendFrameworks }}</div>
  <tags-input
    :selected-tags="backendFrameworks"
    @change="backendFrameworks = [...$event]"
  />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
