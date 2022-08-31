<template lang="">
  <div class="container" :style="style">
    <img src="../assets/search.svg" alt="" />
    <div class="tag-container">
      <ul>
        <li v-for="item in selectedItem" :key="item.id">
          {{ item }}
          <img src="../assets/times.svg" alt="" @click="removeTag(item)" />
        </li>
      </ul>
    </div>
    <input
      :placeholder="placeholder"
      v-model="searchedString"
      @input="filterList"
      type="text"
      name="item-input"
    />
  </div>
  <div class="dropdown">
    <div
      class="dropdown__item"
      v-for="item in filteredList"
      :key="item.code"
      @click="addTag(item.name)"
    >
      {{ item.name }}
    </div>
  </div>
</template>
<script>
export default {
  name: "DropdownInput",
  props: {
    placeholder: {
      type: String,
      default: "Nhập tên cần tìm kiếm",
    },
    listArray: {
      type: Array,
      required: true,
    },
    width: {
      type: String,
      default: "auto",
    },
    height: {
      type: String,
      default: "auto",
    },
  },
  data() {
    return {
      searchedString: "",
      filteredList: [],
      selectedItem: [],
    };
  },
  methods: {
    filterList() {
      if (this.searchedString.length > 0) {
        this.filteredList = [...this.listArray];
        this.filteredList = this.filteredList.filter((item) =>
          item.name.toLowerCase().includes(this.searchedString.toLowerCase())
        );
      } else this.filteredList = [];
    },
    addTag(itemName) {
      if (!this.selectedItem.includes(itemName)) {
        this.selectedItem.push(itemName);
      }
      this.searchedString = "";
      this.filteredList = [];
    },
    removeTag(itemName) {
      this.selectedItem = this.selectedItem.filter((item) => item !== itemName);
    },
  },
  computed: {
    style() {
      return { width: this.width, height: this.height };
    },
  },
};
</script>
<style lang="scss" scoped>
.container {
  height: auto;
  border-radius: 4px;
  border: 1px solid #dbdbdb;
  background: rgba(230, 249, 255, 0.2);
  margin-left: auto;
  margin-right: auto;
  display: flex;
  align-items: center;
  flex-wrap: wrap;

  & img {
    width: 20px;
    height: 20px;
    margin: 12.5px 4px 12.5px 10px;
  }
}
.tag-container {
  display: flex;
  & ul {
    display: flex;
    padding: 0px;
    text-align: left;
    flex-wrap: wrap;
  }

  & li {
    background: #f0f4f8;
    border: 1px solid #dcdcdc;
    border-radius: 4px;
    padding: 4px 0px 4px 8px;
    list-style: none;
    margin: 8px 4px 8px 0px;
    font-family: "Noto Sans";
    font-size: 14px;
    color: #627d98;
    line-height: 20px;
  }

  & img {
    width: 15px;
    height: 15px;
    margin-top: auto;
    margin-bottom: auto;
    margin-left: 0px;
    margin-right: 0px;
    &:hover {
      cursor: pointer;
    }
  }
}
input {
  flex: 1;
  height: 48px;
  border: none;
  background: rgba(230, 249, 255, 0.2);
  font-family: "Noto Sans";
  font-size: 14px;

  &:focus {
    outline: none;
  }
}

.dropdown {
  display: flex;
  flex-direction: column;
  font-family: "Noto Sans";
  margin-left: auto;
  margin-right: auto;
  width: 400px;
  height: 126px;
  overflow: auto;
  &__item {
    text-align: left;
    padding: 10px;
    gap: 10px;
    color: #486581;
    background-color: #f1f5f8;
    &:first-child {
      border-radius: 4px 4px 0px 0px;
    }
    &:last-child {
      border-radius: 0px 0px 4px 4px;
    }

    &:hover {
      cursor: pointer;
      color: #ffffff;
      background-color: #617d98;
    }
  }
}
</style>
