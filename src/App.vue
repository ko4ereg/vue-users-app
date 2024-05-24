<script>
import { ref, onMounted } from 'vue';
import axios from 'axios';
export default {
  setup() {
    const users = ref([]);
    onMounted(() => {
      axios.get('https://jsonplaceholder.typicode.com/users')
        .then(response => {
          users.value = response.data;
        })
        .catch(error => {
          console.error(error)
        });
    });
    return { users }
  }
}
</script>


<template>
  <router-view :users="users" />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

 
</style>
