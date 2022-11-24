<template>
<div class="home">
    <Navbar />
    <!-- Content -->
    <div class="container">
        <Hero />

        <div class="row mt-4">
            <div class="col">
                <h2>Best <strong class="text-primary">Favorite Food</strong> </h2>
            </div>
            <div class="col">
                <router-link to="/menu" class="btn btn-primary float-right">
                    <b-icon icon="eye-fill" class="mr-2"></b-icon>View All
                </router-link>
            </div>
        </div>

        <div class="row mb-4">
            <div class="col-md-4 mt-4" v-for="product in products" :key="product.id">
                <CardProduct :product="product" />
            </div>
        </div>

    </div>
    <!-- End Content -->
</div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import Hero from '@/components/Hero.vue'
import CardProduct from '@/components/CardProduct.vue'
import axios from "axios"

export default {
    name: 'HomeView',
    components: {
        Navbar,
        Hero,
        CardProduct
    },

    data() {
        return {
            products: []
        }
    },

    methods: {
        setProduct(data) {
            this.products = data
        }
    },

    mounted() {
        // Make a request for a user with a given ID
        axios.get('http://localhost:3000/best-products')
            .then((response) =>
                // handle success
                this.setProduct(response.data)
            )
            .catch((error) =>
                // handle error
                console.log(error)
            )
    }
}
</script>
