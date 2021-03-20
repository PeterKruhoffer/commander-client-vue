<template>
  <div class="card" v-for="command in commands" :key="command._id">
    <Command
      @delete-command="$emit('delete-command', command._id)"
      :command="command"
    />
  </div>
</template>

<script>
import Command from "./Command.vue";

export default {
  props: {
    commands: Array,
  },
  components: {
    Command,
  },
  emits: ["delete-command"],
};
</script>

<style>
.card {
  text-align: center;
  box-shadow: 0 4px 8px 2px rgba(29, 70, 124, 0.2);
  width: 90%;
  height: 10rem;
  margin: 3rem auto;
}
</style>
