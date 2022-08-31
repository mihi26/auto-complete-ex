<script>
import DropdownInput from "./components/DropdownInput.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    DropdownInput,
  },
  data() {
    return {
      cityList: [],
    };
  },
  methods: {
    async fetchCityApi() {
      try {
        await axios
          .get("https://provinces.open-api.vn/api/")
          .then((res) => (this.cityList = [...res.data]));
      } catch (e) {
        console.log("Failed to fetch data");
      }
    },
  },
  created() {
    this.fetchCityApi();
  },
};
</script>

<template>
  <div class="app">
    <DropdownInput
      placeholder="Nhập tên thành phố cần tìm kiếm"
      :listArray="cityList"
      width="400px"
    />
  </div>
</template>

<style lang="scss">
* {
  margin: 0;
  box-sizing: border-box;
}
.app {
  margin-top: 140px;
  text-align: center;
}
</style>
