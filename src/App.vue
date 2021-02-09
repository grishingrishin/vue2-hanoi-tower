<template>
    <Towers />
</template>

<script>
import Towers from './components/Towers.vue';

export default {
    name: 'App',
    components: {
        Towers,
    },
};
</script>

<style>
*,
*::before,
*::after {
    box-sizing: border-box;
}

body {
    margin: 0;
}

ul {
    margin: 0;
    padding: 0;
    list-style: none;
}

p {
    margin: 0;
}

a {
    text-decoration: none;
    color: inherit;
}

button {
    margin: 0;
    padding: 0;
    background-color: transparent;
    border: none;
    outline: none;
    cursor: pointer;
}

#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
}
</style>
