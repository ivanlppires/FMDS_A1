<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <v-text-field clearable label="Pesquisar" prepend-icon="mdi-magnify" variant="underlined" v-model="search">
    </v-text-field>
    <v-card>

        <v-list lines="three">
            <v-list-item v-for="(item, index) in filteredItems" :key="index" :title="item.name" :subtitle="item.role"
                :prepend-avatar="item.avatar">
            </v-list-item>
        </v-list>
    </v-card>
</template>
<script setup>
import { ref, computed } from 'vue'
const items = ref([])
const search = ref('')
items.value = [
    { name: 'João', role: 'Chefe', avatar: 'https://randomuser.me/api/portraits/men/1.jpg' },
    { name: 'Maria', role: 'Secretária', avatar: 'https://randomuser.me/api/portraits/women/1.jpg' },
    { name: 'José', role: 'Gerente', avatar: 'https://randomuser.me/api/portraits/men/2.jpg' }
]

const filteredItems = computed(() => {
    return items.value.filter(item => item.name.normalize('NFD').replace(/[\u0300-\u036f]|-/g, "").toLowerCase().startsWith(search.value.normalize('NFD').replace(/[\u0300-\u036f]|-/g, "").toLowerCase()))
});
</script>