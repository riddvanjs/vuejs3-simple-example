<template>
  <form @submit.prevent="addUser">
    <input title="Naam" placeholder="Naam" required type="text" v-model="name">
    <input title="Leeftijd" placeholder="Leeftijd" required type="number" v-model="age">
    <button type="submit">Toevoegen</button>
  </form>
</template>

<script>
import { ref } from 'vue';

export default {
  emits: ['addUser'],
  setup(props, ctx) {
    const name = ref('');
    const age = ref(null);

    function addUser() {
      const user = { name: name.value, age: age.value };
      ctx.emit('addUser', user);
      name.value = '';
      age.value = null;
    }

    return {
      name,
      age,
      addUser
    }
  }
}
</script>

<style lang="scss" scoped>
form {
  display: flex;
  flex-direction: column;
  input {
    margin: 0 0 1rem 0;
    height: 32px;
    border-radius: 0;
    border: 1px solid #ccc;
    text-indent: 1rem;
    font-family: 'Lato', sans-serif;
    font-weight: 400;
    &:focus {
      outline-color: coral;
    }
  }

  button {
    cursor: pointer;
    height: 32px;
    border-radius: 0;
    background-color: transparent;
    border: 1px solid coral;
    color: coral;
    font-weight: 700;
    transition: all .25s ease-in;
    &:hover {
      background-color: coral;
      color: white;
    }
  }
}
</style>
