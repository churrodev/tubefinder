<script setup lang="ts">
    import { ref } from 'vue';

    // Definir los parámetros de la consulta
    const keyword = ref('hotmart');
    const maxResults = ref(20);
    const page = ref(2);
    const perPage = ref(10);

    // Realizar la petición usando useFetch
    const { data, pending, error } = useFetch(() =>
        `/search_videos/`,
        {
            baseURL: 'http://127.0.0.1:8000',
            params: {
                keyword: keyword.value,
                max_results: maxResults.value,
                page: page.value,
                per_page: perPage.value
            }
        }
    );
</script>

<template>
    <div>
        <h2>Search Videos</h2>
        <div v-if="pending">Loading...</div>
        <div v-else-if="error">Error: {{ error.message }}</div>
        <div v-else>
            <ul>
                <li v-for="video in data" :key="video.id">{{video}}</li>
            </ul>
        </div>
    </div>
</template>

<style scoped>

</style>