<template>
<div class="home">
    <Navbar />
    <!-- Content -->
    <div class="container">
      <Hero/>
    </div>
    <!-- End Content -->
</div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import Hero from '@/components/Hero.vue'

export default {
    name: 'HomeView',
    components: {
        Navbar,
        Hero
    }
}
</script>
