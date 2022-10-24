<template>
    <v-app>
        <Nav />
        <v-main>
            <router-view />
        </v-main>
    </v-app>
</template>

<script>
import Nav from '@/components/layouts/Nav'
export default {
    name: 'App',
    components: {
        Nav,
    },
};
</script>
