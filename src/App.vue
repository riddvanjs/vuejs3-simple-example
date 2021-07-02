<template>
  <Form @addUser="addUser" />
  <Users @selectedUser="selectedUser" @deleteUser="deleteUser" :users="users"/>
  <div v-if="Object.keys(selected).length !== 0 && selected.name !== ''">
    <h5>Geselecteerd:</h5>
    {{ selected.name }} - {{ selected.age }}
  </div>
</template>

<script>
import { reactive } from 'vue'
import Form from '@/components/Form'
import Users from '@/components/Users'

export default {
  components: {
    Form,
    Users
  },
  name: 'App',
  setup() {
    const users = reactive([])
    const selected = reactive({})

    function addUser (user) {
      users.push(user);
    }

    function deleteUser(user) {
      users.splice(users.indexOf(user), 1);
      selected.name = '';
      selected.age = '';
    }

    function selectedUser(user) {
      Object.assign(selected, user);
    }

    return {
      users,
      selected,
      addUser,
      selectedUser,
      deleteUser
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@300;400&display=swap');

body {
  font-family: 'Lato', sans-serif;
}
</style>
