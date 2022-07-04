<template>
  <div class="container">
    <drop-down :provinces="provinces" />
  </div>
</template>

<script>
import DropDown from "./components/DropDown.vue";

export default {
  components: { DropDown },
  name: "App",
  data() {
    return {
      provinces: [
        { id: 1, name: "Hà Nội" },
        { id: 2, name: "Hưng Yên" },
        { id: 3, name: "Tp HCM" },
        { id: 4, name: "Nam Định" },
        { id: 5, name: "Thanh Hóa" },
        { id: 6, name: "Nghệ An" },
      ],
    };
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300;400&family=Roboto:wght@100;300;500;700&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
html {
  font-size: 62.5%;
}

.container {
  font-family: 'Open Sans', sans-serif;
  font-size: 1.6rem;
  margin-top: 40px;
  display: flex;
  justify-content: center;
  color: #333333;
}
</style>
