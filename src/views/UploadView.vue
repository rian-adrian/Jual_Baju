<template>
    <div>
      <form @submit.prevent="submitForm">
        <div class="form-group">
          <label for="name">Nama</label>
          <input type="text" class="form-control" id="name" v-model="product.name">
        </div>
        <div class="form-group">
          <label for="description">Deskripsi</label>
          <textarea class="form-control" id="description" v-model="product.description"></textarea>
        </div>
        <div class="form-group">
          <label for="price">Harga</label>
          <input type="number" class="form-control" id="price" v-model="product.price">
        </div>
        <div class="form-group">
            <label for="image">Gambar</label>
            <input type="file" class="form-control-file" id="image" @change="handleFileUpload">
            <img v-if="imagePreview" :src="imagePreview" alt="Preview" style="max-width: 200px;">
        </div>
        <button type="submit" class="btn btn-primary">Simpan</button>
      </form>
    </div>
  </template>
  
  <script>

  import axios from 'axios';

  export default {
  data() {
    return {
      product: {
        name: '',
        description: '',
        price: 0,
        image: null,
      },
      imagePreview: null,
    };
  },
  methods: {
    handleFileUpload(e) {
      const file = e.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = (event) => {
          this.imagePreview = event.target.result;
          this.product.image = file;
        };
        reader.readAsDataURL(file);
      } else {
        this.imagePreview = null;
        this.product.image = null;
      }
    },
    async submitForm() {
      try {
        // Kirim data produk ke server Anda
        const response = await axios.post('/api/upload', this.product);

        // Jika pengiriman berhasil, simpan gambar ke direktori public/images
        if (response.data.success) {
          const formData = new FormData();
          formData.append('image', this.product.image);

          await axios.post('/api/upload-image', formData);

          // Lakukan sesuatu setelah gambar berhasil diunggah
          console.log('Gambar berhasil diunggah');
        } else {
          console.error('Terjadi kesalahan saat mengirim data produk.');
        }
      } catch (error) {
        console.error('Terjadi kesalahan:', error);
      }
    },
  },
};
</script>