<template>
  <div class="tags-input-wrapper">
    <span class="tag-item" v-for="(tag, index) in tags" :key="index">
      {{ tag }}
      <a class="remove-tag" @click.prevent="removeTag(index)" href="#"
        >&times;</a
      >
    </span>
    <hr />
    <input
      class="tag-input"
      type="text"
      v-model.trim="newTag"
      @keydown.enter="addNewTag"
      @keydown.delete="removeLastTag"
      @keydown.tab.prevent="addNewTag"
      :class="{ 'tag-exists': isTagExists }"
    />
  </div>
</template>

<script>
export default {
  //Nơi lưu trữ trạng thái State
  data() {
    return {
      tags: [...this.selectedTags],
      newTag: "",
    };
  },
  props: {
    selectedTags: {
      type: Array,
      default: () => [],
    },
  },

  // watch dùng để theo dõi sự thay đổi của một biến (trong data hoặc computed).
  // Mỗi khi newTag thay đổi (tức là bạn đang gõ trong <input>), hàm newTag(newVal) sẽ chạy.
  watch: {
    newTag(newVal) {
      if (newVal.indexOf(",") > -1) {
        this.newTag = this.newTag.slice(0, -1);
        this.addNewTag();
      }
    },
  },

  // Tự động cập mỗi khi tags hoặc newTag thay đổi
  // Trả về true nếu newTag đã tồn tại trong tags <=> false
  // Dùng để tránh thêm trùng tag và đổi giao diện input khi bị trùng
  computed: {
    isTagExists() {
      return this.tags.includes(this.newTag);
    },
  },
  emits: ["change"],
  methods: {
    addNewTag() {
      if (this.newTag && !this.isTagExists) {
        this.tags.push(this.newTag);
        this.newTag = "";
        this.$emit("change", this.tags);
      }
    },
    removeTag(index) {
      this.tags.splice(index, 1);
      this.$emit("change", this.tags);
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
.tag-input.tag-exists {
  color: red;
  text-decoration: line-through;
}
.tags-input-wrapper {
  background: #fff;
  padding: 0.5em;
  border: 1px solid #dbdbdb;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  min-height: 36px;
  box-sizing: border-box;
}

.tag-item {
  color: #212529;
  background-color: #eee;
  margin-right: 0.3em;
  padding: 0.25em 0.4em;
  font-size: 75%;
  line-height: 1;
  text-align: center;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  padding-right: 1.25em;
  padding-left: 0.6em;
}

.tag-input {
  color: #495057;
  flex: 1;
  background: transparent;
  border: none;
}

.tag-input:focus {
  outline: none;
}
a.remove-tag {
  text-decoration: none;
}
</style>
