<template lang="">
  <div class="container">
    <img src="../assets/search.svg" alt="" />
    <TagInput>
      <div class="tag-container">
        <ul>
          <li v-for="(city, key) in selectedCity" :key="key">
            {{ city }}
            <img src="../assets/times.svg" alt="" @click="removeTag(city)" />
          </li>
        </ul>
      </div>
    </TagInput>
    <input
      placeholder="Nhập tên thành phố để tìm kiếm..."
      v-model="this.searchedCity"
      @input="filterList"
      type="text"
      key="city-input"
    />
  </div>
  <div class="dropdown">
    <div
      class="dropdown__item"
      v-for="city in filteredList"
      :key="city.code"
      @click="addTag(city.name)"
    >
      {{ city.name }}
    </div>
  </div>
</template>
<script>
import TagInput from "./TagInput.vue";
export default {
  name: "DropdownInput",
  components: {
    TagInput,
  },
  data() {
    return {
      cityList: [],
      searchedCity: "",
      filteredList: [],
      selectedCity: [],
    };
  },
  created() {
    fetch("https://provinces.open-api.vn/api/")
      .then((res) => res.json())
      .then((data) => {
        for (let item of data) {
          this.cityList.push(item);
        }
      });
  },
  methods: {
    filterList() {
      if (this.searchedCity.length > 0) {
        this.filteredList = [...this.cityList];
        this.filteredList = this.filteredList.filter((city) =>
          city.name.toLowerCase().includes(this.searchedCity.toLowerCase())
        );
      } else this.filteredList = [];
    },
    addTag(cityName) {
      if (!this.selectedCity.includes(cityName)) {
        this.selectedCity.push(cityName);
      }
      this.searchedCity = "";
      this.filteredList = [];
    },
    removeTag(cityName) {
      this.selectedCity = this.selectedCity.filter((city) => city !== cityName);
    },
  },
};
</script>
<style lang="scss" scoped>
.container {
  width: 400px;
  height: auto;
  border-radius: 4px;
  border: 1px solid #dbdbdb;
  background: rgba(230, 249, 255, 0.2);
  margin-left: auto;
  margin-right: auto;
  display: flex;
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
