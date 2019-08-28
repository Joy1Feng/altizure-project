<template>
    <div id="app">
        <Obj/>
    </div>
</template>

<script>
import Obj from './components/Obj/Obj'
export default {
    name: 'app',
    components: {
        Obj
    }
}
</script>

<style>
    * {
        margin: 0;
        padding: 0;
    }

    html, body {
        width: 100%;
        height: 100%;
    }

    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        width: 100%;
        height: 100%
    }

    #page-content {
        width: 100%;
        height: 100%;
    }
</style>
