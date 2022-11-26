<template>
<div class="keranjang">
    <Navbar :updateKeranjang="keranjangs"/>
    <div class="container mt-4">
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
                        <li class="breadcrumb-item active text-primary" aria-current="page">Keranjang</li>
                    </ol>
                </nav>
            </div>
        </div>

        <!-- Content -->
        <div class="row mt-3">
            <div class="col">
                <h2>Keranjang <strong class="text-primary">Ku..</strong></h2>
                <div class="table-responsive mt-3">
                    <table class="table table-hover table-bordered">
                        <thead>
                            <tr>
                                <th scope="col">#</th>
                                <th scope="col">Foto</th>
                                <th scope="col">Makanan</th>
                                <th scope="col">Keterangan</th>
                                <th scope="col">Jumlah Pesanan</th>
                                <th scope="col">Harga</th>
                                <th scope="col">Total Harga</th>
                                <th scope="col">Hapus</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(keranjang, index) in keranjangs" :key="keranjang.id">
                                <th>{{index+1}}</th>
                                <td>
                                    <img :src="'../assets/image/'+keranjang.products.gambar" class="img-fluid shadow" width="230" alt="">
                                </td>
                                <td><strong>{{keranjang.products.nama}}</strong></td>
                                <td>
                                    {{keranjang.keterangan ? keranjang.keterangan : "-" }}
                                </td>
                                <td>{{keranjang.jumlah_pemesanan}}</td>
                                <td align="right">Rp.{{keranjang.products.harga}}</td>
                                <td align="right">
                                    <strong>Rp.{{keranjang.products.harga*keranjang.jumlah_pemesanan}}</strong>
                                </td>
                                <td align="center">

                                    <b-icon icon="trash-fill" class="text-danger" @click="hapusKeranjang(keranjang.id)"></b-icon>

                                </td>
                            </tr>

                            <tr>
                                <td colspan="6" align="right">
                                    <strong>Total Harga :</strong>
                                </td>
                                <td align="right">
                                    <strong>Rp.{{totalHarga}}</strong>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</div>
</template>

<script>
import Navbar from '@/components/Navbar.vue'
import axios from "axios"

export default {
    name: "KeranjangView",
    components: {
        Navbar,
    },
    data() {
        return {
            keranjangs: []
        }
    },
    methods: {
        setKeranjangs(data) {
            this.keranjangs = data
        },
        hapusKeranjang(id) {
            axios.delete("http://localhost:3000/keranjangs/" + id)
                .then(() => {
                    this.$toast.success('Berhasil Menghapus', {
                        // optional options Object
                        type: 'success',
                        position: 'top-right',
                        duration: 2000,
                        dismissible: true
                    })
                    // Reaload Halaman
                    axios.get("http://localhost:3000/keranjangs")
                        .then((response) => this.setKeranjangs(response.data))
                        .catch((error) => console.log(error))
                })
                .catch((error) => console.log(error))
        }
    },
    mounted() {
        // Make a request for a user with a given ID
        axios.get("http://localhost:3000/keranjangs")
            .then((response) => this.setKeranjangs(response.data))
            .catch((error) => console.log(error))
    },
    computed: {
        totalHarga() {
            return this.keranjangs.reduce(function (items, data) {
                return items + (data.products.harga * data.jumlah_pemesanan)
            }, 0)
        }
    }
}
</script>

<style>

</style>
