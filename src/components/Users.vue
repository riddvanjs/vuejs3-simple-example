<template>
  <ul v-if="hasUsers">
    <li v-for="(user, index) in allUsers" :key="index">
      <div @click="selectedUser(user)" class="meta">
        <span>{{ user.name }} - {{ user.age }}</span>
      </div>
      <button @click="deleteUser(user)">
        <span>x</span>
      </button>
    </li>
  </ul>
  <span class="text-caption" v-else>Nog geen gebruikers..</span>
</template>

<script>
import { reactive, computed } from 'vue'

export default {
  props: ['users'],
  emits: ['deleteUser', 'selectedUser'],
  setup(props, ctx) {
    const allUsers = reactive(props.users);

    function deleteUser(user) {
      ctx.emit('deleteUser', user);
    }

    function selectedUser(user) {
      ctx.emit('selectedUser', user);
    }

    const hasUsers = computed(() => allUsers.length !== 0);

    return {
      allUsers,
      hasUsers,
      selectedUser,
      deleteUser
    }
  }
}
</script>

<style lang="scss" scoped>
span.text-caption {
  display: block;
  margin: 1rem 0 0 0;
  color: #7f7f7f;
}

ul {
  padding-inline-start: 0;
  list-style: none;
  width: 50%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  li {
    &:not(:first-child) {
      margin-top: 1rem;
    }
    cursor: pointer;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    transition: all .25s ease-in;
    .meta {
      width: 100%;
      text-align: center;
    }
    button {
      cursor: pointer;
      border: none;
      background-color: coral;
      color: white;
      padding: .7rem;
      display: flex;
      align-items: center;
    }

    &:hover {
      background-color: #ccc;
    }
  }
}

</style>
