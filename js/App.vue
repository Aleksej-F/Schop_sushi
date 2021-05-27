<template>
    <div id="app" > 
        <Header/>
        <Slider/>
        <Navigation/>
    </div>
</template>

<script>
import Header from './components/Header.vue'
import Slider from './components/Slider.vue'
import Navigation from './components/Navigation.vue'
export default {
    name: 'App',
    components: {
        Header,
        Slider,
        Navigation
    },
}
</script>