<script lang="ts" setup>
const key = 'apikey=ff0d50dd'
const url = `http://www.omdbapi.com/?`

const query = ref("");
const movies = ref<any[]>([])

const search = async () => {
    const fullUrl = url + `s=${query.value}&${key}`;
    console.log('Full URL:', fullUrl);
    // @ts-ignore
    const { Search } = await $fetch(fullUrl)
    console.log('Search:', Search);
    movies.value = Search;
}
</script>

<template>
    <div>
        <form @submit.prevent="search">
            <input type="text" v-model="query">
            <button>Search</button>
        </form>

        <ul style="display:flex; flex-wrap:wrap; gap:10px; list-style:none;">
            <li v-for="movie in movies" :key="movie.imdbID">
                <NuxtLink v-if="!!movie.imdbID" :to="{ name: 'movies-id', params: { id: movie.imdbID } }">
                    <img :src="movie.Poster" :alt="movie.Title" />
                </NuxtLink>
            </li>
        </ul>
    </div>
</template>