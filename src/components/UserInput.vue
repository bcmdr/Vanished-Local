<template>
  <form @submit.prevent="logInput()">
    <input type="text" v-model="inputText" placeholder="Type Here..." class="user-input">
    <button @click.prevent="handleSubmitClick" type="submit" :class="{ active: inputText }">Enter</button>
  </form>
</template>

<script>
export default {
  name: "UserInput",
  data() {
    return {
      inputText: ""
    };
  },
  methods: {
    handleSubmitClick() {
      if (this.inputText) {
        this.logInput();
      } else {
        document.querySelector(".user-input").focus();
      }
    },
    logInput() {
      // Trim Whitespace and cancel if empty
      let input = this.inputText.trim();
      if (!input) return;

      this.$store.dispatch("logInput", input.toLowerCase());
      this.$store.dispatch("addOutput", input);

      this.inputText = "";
    }
  }
};
</script>

<style scoped>
form {
  color: white;
  display: flex;
  padding: 8px;
  border-bottom: 1px solid white;
}

input[type="text"] {
  color: white;
  flex-grow: 1;
  padding: 10px;
  border: none;
  margin-right: 10px;
  font-size: 0.8rem;
  background: transparent;
}

button {
  color: #111;
  border: 1px solid white;
  background: #eee;
  font-size: 0.8rem;
}
</style>
