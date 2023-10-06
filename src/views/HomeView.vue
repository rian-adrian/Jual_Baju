<template>
 <div id="app">
        <div class="products-section">
            <!-- Bagian Produk (Sebelah Kiri) -->
            <div class="products">
                <div class="product" v-for="(product, index) in products" :key="index">
                    <div class="product-image">
                        <!-- Menggunakan dynamic binding untuk mengganti nama file gambar -->
                        <img :src="'/images/' + product.image" alt="Baju">
                    </div>
                    <div class="product-info">
                        <h2>{{ product.name }}</h2>
                        <p>{{ product.description }}</p>
                        <p>Harga: ${{ product.price }}</p>
                        <button @click="addToCart(index)" class="btn btn-outline-success">Tambah ke Keranjang</button>
                    </div>
                </div>
            </div>

            <!-- Bagian Keranjang Belanja (Sebelah Kanan) -->
            <div class="cart-section">
              <div class="cart">
                <h2>Keranjang Belanja</h2>
                <transition-group name="cart-fade" tag="ul">
                  <li v-for="(item, index) in cart" :key="index" class="cart-item">
                    <span>{{ item.name }}</span>
                    <span class="price">${{ item.price }}</span>
                    <button @click="removeFromCart(index)" class="btn btn-danger">Hapus</button>
                  </li>
                </transition-group>
              </div>
            </div>
        </div>
    </div>

</template>
<style>
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
}

.products-section {
    display: flex;
}

.products {
    flex: 1;
    padding: 20px;
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}

.product {
    width: 200px;
    border: 1px solid #ccc;
    padding: 10px;
    transition: transform 0.3s ease;
}

.product:hover {
    transform: scale(1.05);
}

.product img {
    width: 100%;
    height: auto;
    margin-bottom: 10px;
}

.cart-section {
    flex: 1;
    padding: 20px;
    background-color: #f2f2f2;
}

.cart {
    background-color: #fff;
    padding: 10px;
    border: 1px solid #ccc;
    max-height: 300px;
    overflow-y: auto;
}

.cart-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #fff;
  padding: 10px;
  margin: 5px 0;
  border: 1px solid #ccc;
  border-radius: 5px;
  opacity: 1;
  transition: opacity 0.5s ease-in-out;
}

.cart-item-enter-active,
.cart-item-leave-active {
  transition: opacity 0.5s;
}

.cart-item-enter, .cart-item-leave-to /* .cart-item-leave-active dalam <2.1.8 */ {
  opacity: 0;
}
</style>
<script>
import HelloWorld from '@/components/HelloWorld.vue';
import Swal from 'sweetalert2'

export default {
  name: 'HomeView',
  components: {
    // eslint-disable-next-line vue/no-unused-components
    HelloWorld
  },
  data() {

    return {
      products: HelloWorld.data().products,
      cart: [],
    };

  },
  methods: {
    addToCart(index) {
      let productToAdd = { ...this.products[index] };
      this.cart.push(productToAdd);
      // console.log(productToAdd);
      Swal.fire({
        icon: 'success',
        title: 'Produk Ditambahkan',
        text: 'Produk telah ditambahkan ke keranjang belanja!',
        confirmButtonText: 'Ok'
      });
    },
    removeFromCart(index) {
      this.cart.splice(index, 1);
    }
  }
};
</script>



