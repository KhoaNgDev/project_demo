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
    :class="{ 'tag-exists': isTagExists }"
  />
</template>

<script>
export default {
  //Nơi lưu trữ trạng thái State
  data: () => ({
    tags: ["vue", "react", "angular"],
    newTag: "",
  }),

  // Tự động cập mỗi khi tags hoặc newTag thay đổi
  // Trả về true nếu newTag đã tồn tại trong tags <=> false
  // Dùng để tránh thêm trùng tag và đổi giao diện input khi bị trùng
  computed: {
    isTagExists() {
      return this.tags.includes(this.newTag);
    },
  },
  methods: {
    addNewTag() {
      if (this.newTag && !this.isTagExists) {
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
