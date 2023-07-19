<script setup lang="ts">
const route = useRoute();

const key = 'apikey=ff0d50dd'
const url = `http://www.omdbapi.com/?`

// Using useAsyncData prevents duplicate server/client fetches
// Key is first argument.  Nuxt caches api requests, but if the key is 
//  different, then it will refetch
const { data } = useAsyncData(`/movies/${route.params.id}`,() => {
    return $fetch(url + `i=${route.params.id}&${key}`)
})

</script>

<template>
    <div>
        <pre>
            {{ data }}
        </pre>
    </div>
</template>