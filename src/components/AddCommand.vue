<template>
  <form @submit="onSubmit">
    <div class="form-control">
      <label>Platform</label>
      <input
        type="text"
        v-model="platform"
        name="platform"
        placeholder="Platform"
      />

      <label>Description</label>
      <input
        type="text"
        v-model="howTo"
        name="howTo"
        placeholder="Description"
      />

      <label>Command Line</label>
      <input
        type="text"
        v-model="line"
        name="line"
        placeholder="Command Line"
      />
    </div>
    <input type="submit" value="Save Command" class="btn" />
  </form>
</template>

<script>
export default {
  data() {
    return {
      platform: "",
      howTo: "",
      line: "",
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();

      if (!this.platform) {
        alert("Please add a platform");
        return;
      }

      const newCommand = {
        platform: this.platform,
        howTo: this.howTo,
        line: this.line,
      };

      this.$emit("new-command", newCommand);

      this.platform = "";
      this.howTo = "";
      this.line = "";
    },
  },
};
</script>

<style>
.form-control {
  margin: 2rem 20rem;
  justify-content: center;
  align-items: center;
}

.form-control label {
  display: block;
  color: #5e739b;
  font-size: 1.5rem;
  text-align: left;
  margin-left: 1rem;
  margin-top: 2rem;
}

.form-control input {
  width: 100%;
  height: 3rem;
  margin: 1rem;
  padding: 3px 7px;
  font-size: 17px;
}

.btn {
  background-color: #336acf;
  border: none;
  color: white;
  text-align: center;
  display: inline-block;
  font-size: 1.5rem;
  padding: 0.5rem 0.6rem;
  border-radius: 12px;
}
</style>