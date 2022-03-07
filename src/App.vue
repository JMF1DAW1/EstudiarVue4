<template>
    <div id="app">
        <h1 class="text-center mb-2">Buscar usuario de GitHub</h1>
        <GitHub></GitHub>
    </div>
</template>

<script>
import GitHub from "./components/GitHub.vue"

export default {
    name: 'App',
    components: {
        GitHub
    }
}
</script>

<style>
</style>
