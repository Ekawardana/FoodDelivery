<template>
    <div class="pesanan-sukses">
        <Navbar/>
        <div class="container">
            <div class="row justify-content-center mt-4">
                <div class="col text-center">
                    <img src="assets/image/loading.png" width="300" alt="">
                    <h2><strong class="text-primary">Yeay! Pesanan Sukses</strong></h2>
                    <h4>Pesanan anda sedang dibuat<br>Selamat Menunggu☺</h4>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue'

export default {
    name: 'PesananSukses',
    components: {
        Navbar,
    },
}
</script>

<style>

</style>