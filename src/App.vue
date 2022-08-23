<script>
import DropdownInput from "./components/DropdownInput.vue";

export default {
  name: "App",
  components: {
    DropdownInput,
  },
};
</script>

<template>
  <div class="app">
    <DropdownInput />
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
