<script>
import axios from 'axios';
import { ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';
export default {
    setup() {
        const route = useRoute();
        const router = useRouter();
        const user = ref(null);
        const goBack = () => {
            router.push({
                name: 'UsersList'
            });
        }

        onMounted(() => {
            // Fetch user data by ID from API 
            axios.get(`https://jsonplaceholder.typicode.com/users/${route.params.id}`)
                .then(response => {
                    user.value = response.data;
                })
                .catch(error => {
                    console.error(error);
                });
        });
        return { user, goBack };
    }
}
</script>

<template>
    <div class="container" v-if="user">
        <button @click="goBack">Назад</button>
        <h1>{{ user.name }}</h1>
        <p>E-mail: {{ user.email }}</p>
        <p>Номер телефона: {{ user.phone }}</p>
        <p>Домашний адрес: {{ user.address.city }}, {{ user.address.street }}, {{ user.address.suite }} </p>
        <p>Сайт: <a href="">{{ user.website }}</a></p>
    </div>
    <div class="container" v-else>Загрузка...</div>
</template>



<style scoped>
body {
    font-family: 'Arial', sans-serif;
    background-color: #f0f0f0;
    margin: 0;
    padding: 0;
}

button {
    outline: none;
    background-color: rgb(245, 222, 179, 0.5);
    border: 1px solid rgba(0, 0, 0, 0.1);
    cursor: pointer;
    border-radius: 8px;
    width: 100px;
}

button:hover {
    background-color: rgb(245, 222, 179, 1);
}

.container {
    max-width: 100%;
    margin: 0 auto;
    padding: 20px;
    background-color: #fff;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h1 {
    color: #333;
    margin-bottom: 10px;
    font-size: 28px;
}

p {
    color: #666;
    margin-bottom: 5px;
    font-size: 16px;
}

@media (max-width: 768px) {
    .container {
        padding: 10px;
        border-radius: 0;
    }

    h1 {

        margin-bottom: 10px;
        font-size: 22px;
    }

    p {

        margin-bottom: 5px;
        font-size: 14px;
    }
}
</style>