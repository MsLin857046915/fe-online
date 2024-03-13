<template>
    <div>
        <org-tree @custom-event="handleCustomEvent"></org-tree>
        <user-table :search="search"></user-table>
    </div>
</template>

<script setup lang="ts">
import orgTree from './orgTree.vue'
import userTable from './userTable.vue'
import { ref } from '@vue/reactivity'

const search = ref({})
const handleCustomEvent = (node) => {
    search.value = node
} 
</script>
