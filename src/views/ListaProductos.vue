<template>
  <div class="container mt-4">
    <h1 class="text-center mb-4">Lista de Productos</h1>
    <div class="row">
      <div
        class="col-12 col-sm-6 col-md-4 col-lg-3 mb-3"
        v-for="product in products"
        :key="product.id"
      >
        <div class="card h-100">
          <img :src="product.image" class="card-img-top" alt="product.title" />
          <div class="card-body">
            <h5 class="card-title">{{ product.title }}</h5>
            <p class="card-text">{{ product.description }}</p>
            <p class="card-text"><strong>Precio: ${{ product.price }}</strong></p>
            <p class="card-text">Rating: {{ product.rating.rate }} ({{ product.rating.count }} reviews)</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';

export default {
  name: 'ListaProductos',
  setup() {
    const products = ref([]);

    const fetchProducts = async () => {
      try {
        const response = await fetch('https://fakestoreapi.com/products');
        const data = await response.json();
        products.value = data;
      } catch (error) {
        console.error('Error fetching products:', error);
      }
    };

    onMounted(() => {
      fetchProducts();
    });

    return {
      products,
    };
  },
};
</script>

<style scoped>
.card-img-top {
  height: 150px;
  object-fit: contain;
}
</style>
