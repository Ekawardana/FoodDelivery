<template>
<div class="menu-detail">
    <Navbar />
    <div class="container">
        <!-- Menu Mini -->
        <div class="row mt-4">
            <div class="col">
                <nav aria-label="breadcrumb">
                    <ol class="breadcrumb">
                        <li class="breadcrumb-item">
                            <router-link to="/" class="text-dark">Home</router-link>
                        </li>
                        <li class="breadcrumb-item">
                            <router-link to="/menu" class="text-dark">Menu</router-link>
                        </li>
                        <li class="breadcrumb-item active text-primary" aria-current="page">Menu Order</li>
                    </ol>
                </nav>
            </div>
        </div>

        <!-- Detail -->
        <div class="row mt-3">
            <div class="col-md-6">
                <img :src="'../assets/image/'+products.gambar" class="img-fluid shadow" alt="..." />
            </div>
            <div class="col-md-6">
                <h2><strong>{{products.nama}}</strong></h2>
                <hr>
                <h4>Harga : <strong>Rp.{{products.harga}}</strong></h4>

                <form class="mt-3" v-on:submit.prevent>
                    <div class="form-group">
                        <label for="jumlah_pemesanan">Jumlah Pesanan</label>
                        <input type="number" class="form-control" v-model="pesanan.jumlah_pemesanan" />
                    </div>
                    <div class="form-group">
                        <label for="jumlah_pemesanan">Keterangan</label>
                        <textarea class="form-control" v-model="pesanan.keterangan" placeholder="Keterangan seperti : Pedas, Nasi Setengah dll.."></textarea>
                    </div>

                    <button class="btn btn-primary" type="submit" @click="pemesanan">
                        <b-icon icon="cart-plus-fill" class="mr-2"></b-icon>Pesan
                    </button>
                </form>
            </div>
        </div>

    </div>
</div>
</template>

<script>
import Navbar from '@/components/Navbar.vue'
import axios from 'axios';

export default {
    name: 'MenuDetail',
    components: {
        Navbar,
    },
    data() {
        return {
            products: {},
            pesanan: {}
        }
    },
    methods: {
        setProduct(data) {
            this.products = data
        },
        pemesanan() {
            if (this.pesanan.jumlah_pemesanan) {
                this.pesanan.products = this.products
                axios
                    .post("http://localhost:3000/keranjangs", this.pesanan)
                    .then(() => {
                        this.$router.push({path:"/keranjang"})
                        this.$toast.success('Sukses Masuk Keranjang', {
                            // optional options Object
                            type: 'success',
                            position: 'top-right',
                            duration: 2000,
                            dismissible: true
                        })
                    })
                    .catch((error) =>
                        // handle error
                        console.log(error)
                    )
            } else {
                this.$toast.error('Oops, Jumlah Pesanan Harus Diisi!!', {
                    // optional options Object
                    type: 'error',
                    position: 'top-right',
                    duration: 2000,
                    dismissible: true
                })
            }
        }
    },
    mounted() {
        // Make a request for a user with a given ID
        axios.get("http://localhost:3000/products/" + this.$route.params.id)
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
