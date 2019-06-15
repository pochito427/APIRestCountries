<template>
  <div id="app">
    <HeaderList></HeaderList>
    <SideBarList></SideBarList>
  </div>
</template>

<script>
import HeaderList from "./components/HeaderList";
import SideBarList from "./components/SideBarList";

export default {
  name: "App",
  components: {
    HeaderList,
    SideBarList
  }
};
</script>

<style>

</style>