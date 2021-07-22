<template>
    <div id="app">
        <v-app>
            <AppNavigation />
            <v-main>
                <v-container fluid class="pr-0 pb-0">
                    <keep-alive include="Home,Search" :max="10">
                        <router-view />
                    </keep-alive>
                </v-container>
            </v-main>
        </v-app>
    </div>
</template>
<script>
import AppNavigation from '@/components/AppNavigation.vue';
export default {
    name: 'App',
    components: { AppNavigation }
};
</script>
<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    padding-right: 20px;
    max-height: 1888px;
    color: #2c3e50;
}

#app .v-navigation-drawer__border {
    background-color: rgba(255, 255, 255, 0.9);
}
</style>
