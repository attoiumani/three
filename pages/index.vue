<template>
  <div id="app">
    <three/>
    <NLink to="/test1" class="button--grey">About</NLink>
  </div>
</template>

<script>
import three from "@/components/three.vue";

export default {
  name: "app",
  components: {
    three
  }
};
</script>

