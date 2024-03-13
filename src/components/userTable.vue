<template>
    <div>
        <input type="text" v-model="searchKeyword" @input="handleSearch(searchKeyword)" placeholder="Search...">
        <table>
            <thead>
                <tr>
                    <th>id</th>
                    <th>Name</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="user in userApiData" :key="user.id">
                    <td>{{ user.id }}</td>
                    <td>{{ user.name }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script setup lang="ts">
import userApi from '../api/user'
import { defineProps, ref, onMounted, watch, toRefs } from 'vue';

const searchKeyword = ref(null)
const userApiData = ref([])
const handleSearch = (node) => {
    userApi.query(node).then((users) => {
        userApiData.value = users
    })
}

const props = defineProps({
    //子组件接收父组件传递过来的值
    search: Object,
})
const { search } = toRefs(props);

watch(search, (newVal, oldVal) => {
    handleSearch(newVal)
});

onMounted(() => {
    handleSearch({})
});
</script>