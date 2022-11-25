<template>
<div class="Navbar">
    <!-- Navbar -->
    <b-navbar toggleable type="light" class="navbar-expand-lg">
        <div class="container">
            <b-navbar-brand href="/">
                <img src="assets/logo.png" width="60px" />
            </b-navbar-brand>

            <b-navbar-toggle target="navbar-toggle-collapse">
                <template #default="{ expanded }">
                    <b-icon v-if="expanded" icon="chevron-bar-up"></b-icon>
                    <b-icon v-else icon="chevron-bar-down"></b-icon>
                </template>
            </b-navbar-toggle>

            <b-collapse id="navbar-toggle-collapse" is-nav>
                <b-navbar-nav class="mr-auto nav-item">
                    <router-link class="nav-link" to="/">Home</router-link>
                    <router-link class="nav-link" to="/menu">Menu</router-link>
                </b-navbar-nav>
                <b-navbar-nav class="ml-auto nav-item">
                    <router-link class="nav-link" to="/keranjang">Keranjang
                        <b-icon icon="bag"></b-icon>
                        <span class="badge badge-primary ml-2">0</span>
                    </router-link>
                </b-navbar-nav>

            </b-collapse>
        </div>
    </b-navbar>
</div>
</template>

<script>
export default {
    name: 'NavbarItem'
}
</script>

<style>

</style>
