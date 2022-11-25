<template>
<div>
    <Navbar />
    <div class="container">
        <div class="row mt-4">
            <div class="col">
                <h2>Daftar <strong class="text-primary">Menu</strong></h2>
            </div>
        </div>

        <div class="row mb-3">
            <div class="col-sm-8">
                <div class="input-group mt-3">
                    <input type="text" v-model="search" class="form-control" placeholder="Cari Makanan.." @keyup="searchMenu" />

                    <b-input-group-append>
                        <b-button variant="primary">
                            <b-icon icon="search"></b-icon>
                        </b-button>
                    </b-input-group-append>
                </div>
            </div>
        </div>

        <div class="row mb-4">
            <div class="col-md-4 mt-4" v-for="product in products" :key="product.id">
                <CardProduct :product="product" />
            </div>
        </div>
    </div>
</div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import CardProduct from '@/components/CardProduct.vue'
import axios from 'axios'

export default {
    name: 'MenuView',
    components: {
        Navbar,
        CardProduct
    },
    data() {
        return {
            products: [],
            search: ''
        }
    },
    methods: {
        setProduct(data) {
            this.products = data
        },

        searchMenu() {
            axios.get(`http://localhost:3000/products/?q=${this.search}`)
                .then((response) =>
                    // handle success
                    this.setProduct(response.data)
                )
                .catch((error) =>
                    // handle error
                    console.log(error)
                )
        }

    },
    mounted() {
        // Make a request for a user with a given ID
        axios.get("http://localhost:3000/products")
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

<style>

</style>
