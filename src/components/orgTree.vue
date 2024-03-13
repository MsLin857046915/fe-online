<template>
    <div>
        <ul>
            <li v-for="node in orgApiData" :key="node.id">
                <span @click="handleNodeSelect(node)">{{ node.name }}</span>
            </li>
        </ul>
    </div>
</template>
<script setup lang="ts">
import orgApi from '../api/org'
import { defineEmits, ref } from 'vue';

const orgApiData = ref([])
const emit = defineEmits(['custom-event']);
orgApi.query().then((users) => {
    orgApiData.value = users
})
const handleNodeSelect = (node) => {
    emit('custom-event', node);
}
</script>