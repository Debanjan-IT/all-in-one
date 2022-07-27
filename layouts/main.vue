<template>
    <div>
        <navbarVue />
        <Nuxt />
    </div>
</template>

<script>
import navbarVue from "../components/navbar.vue";
export default {
    name: 'main',
    components: {
        navbarVue
    }
}
</script>