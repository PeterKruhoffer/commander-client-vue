<template>
  <div class="container">
    <div class="card-btn">
      <button @click="$emit('delete-command', command._id)" class="btn-delete">
        X
      </button>
    </div>
    <ul>
      <h2>{{ command.platform }}:</h2>
      <li>{{ command.howTo }}:</li>
      <li>{{ command.line }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    command: Object,
  },
  emits: ["delete-command"],
};
</script>

<style scoped>
body {
  display: flex;
  justify-content: center;
  align-items: center;
}

h1 {
  margin-top: 4rem;
  font-size: 4rem;
}

h2 {
  color: #5e739b;
  text-align: left;
}

li {
  list-style: none;
  float: left;
  font-size: 20px;
  padding: 5px 20px 20px 0px;
}

i {
  padding-right: 1rem;
  color: rgb(45, 97, 209);
}

.container {
  line-height: 1.6;
}

.card-btn {
  float: right;
}

.btn-delete {
  background-color: #c44343;
  border: none;
  color: white;
  text-align: center;
  font-size: 1.5rem;
  padding: 0.2rem 0.5rem;
  float: right;
}
</style>
