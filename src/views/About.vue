<template>
  <div class="about">
  <!-- <h1>This is an about page</h1> -->
  <HelloWorld msg="This is an About page" />
</div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue"; //child component

export default {
  name: "About",
  components: {
    HelloWorld
  }
};
</script>
