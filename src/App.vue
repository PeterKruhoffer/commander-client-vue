<template>
  <img alt="Vue logo" src="./assets/logo.png" class="logo" />
  <h1>Commander!</h1>
  <i @click="toggleAddCommand" class="fas fa-plus fa-2x icon"></i>
  <AddCommand v-show="showAddCommand" @new-command="newCommand" />
  <ListOfCommands @delete-command="deleteCommand" :commands="commands" />
</template>

<script>
import AddCommand from "./components/AddCommand";
import ListOfCommands from "./components/ListOfCommands";

const API_URL = "http://localhost:5000/commands";

export default {
  data() {
    return {
      commands: [],
      showAddCommand: false,
    };
  },
  methods: {
    async newCommand(command) {
      const res = await fetch(API_URL, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(command),
      });

      if (res.status === 201) {
        this.commands = [...this.commands, command];
      }
    },
    async getCommands() {
      const response = await fetch(API_URL);

      const data = await response.json();

      return data;
    },
    async deleteCommand(id) {
      if (confirm("Are you sure")) {
        const response = await fetch(API_URL + "/" + id, {
          method: "DELETE",
        });
        response.status === 200
          ? (this.commands = this.commands.filter(
              (command) => command._id !== id
            ))
          : alert("Error deleting command");
      }
    },
    toggleAddCommand() {
      this.showAddCommand = !this.showAddCommand;
    },
  },
  async created() {
    this.commands = await this.getCommands();
  },
  components: {
    ListOfCommands,
    AddCommand,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #a7a8a8;
  margin-top: 60px;
}

@keyframes color-rotate {
  from {
    filter: hue-rotate(0deg);
  }
  to {
    filter: hue-rotate(360deg);
  }
}

.logo:hover {
  animation: color-rotate 1s;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}

.icon {
  color: #336acf;
  float: left;
  margin-left: 4rem;
  margin-top: -1rem;
}
</style>
