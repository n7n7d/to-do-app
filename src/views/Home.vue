<template>
  <div class="columns">
    <div class="column is-4 is-offset-4">
      <ToDo />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import ToDo from "@/components/todo.vue";

export default {
  name: "Home",
  components: {
    ToDo,
  },
};
</script>
