<template>
  <div class="container mt-4">
    <h1 class="text-center mb-4">Lista de Productos</h1>
    
    <!-- Mostrar mensaje de cargando si aún no se ha recibido la respuesta de la API -->
    <div v-if="isLoading" class="text-center">
      <p>Cargando productos...</p>
    </div>

    <!-- Mostrar productos una vez que estén cargados -->
    <div v-else class="row">
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
    const isLoading = ref(true); // Estado de carga

    const fetchProducts = async () => {
      try {
        const response = await fetch('https://fakestoreapi.com/products');
        const data = await response.json();
        products.value = data;
      } catch (error) {
        console.error('Error fetching products:', error);
      } finally {
        isLoading.value = false; // Cambiar el estado de carga cuando los productos estén listos
      }
    };

    onMounted(() => {
      fetchProducts();
    });

    return {
      products,
      isLoading, // Retorna el estado de carga para usarlo en el template
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
