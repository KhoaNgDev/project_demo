<template>
  <div v-for="(tag, index) in tags" :key="index">
    {{ tag }}
    <a @click.prevent="removeTag(index)" href="#">&times;</a>
  </div>
  <hr />
  {{ newTag }}
  <input
    type="text"
    v-model.trim="newTag"
    @keydown.enter="addNewTag"
    @keydown.delete="removeLastTag"
    @keydown.tab.prevent="addNewTag"
    :class="{ 'tag-exists': tags.includes(newTag) }"
  />
</template>

<script>
export default {
  data: () => ({
    tags: ["vue", "react", "angular"],
    newTag: "",
  }),
  methods: {
    addNewTag() {
      if (this.newTag) {
        this.tags.push(this.newTag);
        this.newTag = "";
      }
    },
    removeTag(index) {
      this.tags.splice(index, 1);
    },
    removeLastTag() {
      if (this.newTag.length === 0) {
        this.removeTag(this.tags.length - 1);
      }
    },
  },
};
</script>
<style scoped>
.tag-exists {
  color: red;
  text-decoration: line-through;
}
</style>
