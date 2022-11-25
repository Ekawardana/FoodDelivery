<template>
<div class="card shadow card-product">
    <img :src="'assets/image/' + product.gambar" class="card-img-top" alt="...">
    <div class="card-body">
        <h5 class="card-title">{{product.nama}}</h5>
        <p class="card-text">Harga : {{product.harga}}</p>
        <router-link class="btn btn-primary" :to="'/menu/'+product.id">
            <b-icon icon="cart4" class="mr-2"></b-icon>Pesan
        </router-link>
    </div>
</div>
</template>

<script>
export default {
    name: 'CardProductView',
    props: ['product']
}
</script>

<style>

</style>
