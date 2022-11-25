<template>
<div class="hero">
    <!-- Dekstop -->
    <div class="d-none d-md-block">
        <div class="row">
            <div class="col-md-6">
                <div class="d-flex h-100">
                    <div class="justify-content-center align-self-center">
                        <h2><strong class="text-primary">Favorite Foods Menu,</strong><br>In Your Gadget</h2>
                        <p>Segera pesan makanan favorit anda sebelum kehabisan!</p>
                        <router-link class="btn btn-lg btn-primary" to="/menu">
                            <b-icon icon="cart-plus" class="mr-2"></b-icon>Pesan
                        </router-link>
                    </div>
                </div>
            </div>
            <div class="col-md-6">
                <img src="assets/image/hero.png" width="100%" />
            </div>
        </div>
    </div>

    <!-- Hp -->
    <div class="d-sm-block d-md-none">
        <div class="row">
            <div class="col-md-6 mb-3">
                <img src="assets/image/hero.png" width="100%" />
            </div>
            <div class="col-md-6">
                <div class="d-flex h-100">
                    <div class="justify-content-center align-self-center">
                        <h2><strong class="text-primary">Favorite Foods Menu,</strong><br>In Your Gadget</h2>
                        <p>Segera pesan makanan favorit anda sebelum kehabisan!</p>
                        <button class="btn btn-lg btn-primary">
                            <b-icon icon="bell-fill" class="mr-2"></b-icon>Pesan
                        </button>
                    </div>
                </div>
            </div>
            
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: 'HeroView'
}
</script>

<style>

</style>
