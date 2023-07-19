<script setup lang="ts">
const route = useRoute();

const key = 'apikey=ff0d50dd'
const url = `http://www.omdbapi.com/?`


const fullUrl = url + `i=${route.params.id}&${key}`;

// Using useAsyncData prevents duplicate server/client fetches
const { data } = useAsyncData(() => {
    return $fetch(fullUrl)
})

</script>

<template>
    <div>
        <pre>
            {{ data }}
        </pre>
    </div>
</template>