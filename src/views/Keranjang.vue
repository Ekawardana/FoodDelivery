<template>
<div class="keranjang">
    <Navbar :updateKeranjang="keranjangs" />
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

        <!-- Form Checkout -->
        <div class="row justify-content-end">
            <div class="col-md-4">
                <form class="mt-3" v-on:submit.prevent>
                    <div class="form-group">
                        <label for="nama">Nama :</label>
                        <input type="text" class="form-control" v-model="pesanan.nama" />
                    </div>

                    <div class="form-group">
                        <label for="noMeja">Nomor Meja :</label>
                        <input type="number" class="form-control" v-model="pesanan.noMeja" />
                    </div>
                    <button class="btn btn-primary float-right" type="submit" @click="checkout">
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
import axios from "axios"

export default {
    name: "KeranjangView",
    components: {
        Navbar,
    },
    data() {
        return {
            keranjangs: [],
            pesanan: {}
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
                    // Update Halaman untuk Navbar
                    axios.get("http://localhost:3000/keranjangs")
                        .then((response) => this.setKeranjangs(response.data))
                        .catch((error) => console.log(error))
                })
                .catch((error) => console.log(error))
        },
        // Checkout
        checkout() {
            if (this.pesanan.nama && this.pesanan.noMeja) {
                this.pesanan.keranjangs = this.keranjangs
                axios.post("http://localhost:3000/pesanans", this.pesanan)
                    .then(() => {
                        // Hapus semua isi keranjang
                        this.keranjangs.map(function (item) {
                            return axios
                                .delete("http://localhost:3000/keranjangs/" + item.id)
                                .catch((error) => console.log(error))
                        })
                        // Semua pesanan masuk ke pesanan-sukses
                        this.$router.push({
                            path: "/pesanan-sukses"
                        })
                        this.$toast.success('Pemesanan Berhasil', {
                            type: 'success',
                            position: 'top-right',
                            duration: 2000,
                            dismissible: true
                        })
                    })
            } else {
                // Jika ada field yang kosong
                this.$toast.error('Oops, Harus Diisi', {
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
        axios.get("http://localhost:3000/keranjangs")
            .then((response) => this.setKeranjangs(response.data))
            .catch((error) => console.log(error))
    },
    // Total seluruh harga
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
