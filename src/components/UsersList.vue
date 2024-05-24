<script>
import { computed, ref } from 'vue';
import { useRouter } from 'vue-router';

export default {
    props: {
        users: Array
    },
    setup(props) {
        const search = ref('')
        const filteredUsers = computed(() => {
            return props.users.filter(user => user.name.toLowerCase().includes(search.value.toLowerCase()) || user.email.toLowerCase().includes(search.value.toLowerCase())
            );
        });

        const router = useRouter();
        const goToUserDetails = (user) => {
            router.push({
                name: 'UserDetails', params: { id: user.id }
            });
        }
        return { search, filteredUsers, goToUserDetails };
    }
}
</script>

<template>
    <div class="list">
        <input type="text" v-model="search" placeholder="Введите имя или E-mail">
        <table>
            <tr>
                <th>Имя</th>
                <th>E-mail</th>
            </tr>
            <tr v-for="user in filteredUsers" :user="user" :key="user.id" @click="goToUserDetails(user)">
                <td>{{ user.name }}</td>
                <td>{{ user.email }}</td>



            </tr>
        </table>

    </div>
</template>

<!-- 
<style scoped>
.list {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 20px;
}

input {
    border: 2px solid #1f1f11;
    border-radius: 8px;
    font-size: 24px;

}
 



</style> -->

<style scoped>
.list {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 20px;
    max-width: 80%;
    margin: 0 auto;
}

input {
    border: 2px solid #1f1f11;
    border-radius: 8px;
    font-size: 24px;
    padding: 10px;
    width: 100%;
    max-width: 400px;
}

table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
}

th,
td {
    border: 1px solid #1f1f11;
    padding: 10px;
}

th {
    background-color: #f0f0f0;
}

tr {
    cursor: pointer;
}

@media (max-width: 768px) {
    input {
        font-size: 18px;
        max-width: 300px;
    }

    th,
    td {
        padding: 8px;
    }
}
</style>