<template>
  <div>
    <h1>Lista de Productos</h1>
    <h2 class="slogan">Encuentra lo mejor en nuestra tienda online</h2>
    
    <!-- Mostrar 'Cargando...' hasta que se obtenga la respuesta del API -->
    <div v-if="loading" class="loading">
      <p>Cargando...</p>
    </div>

    <!-- Mostrar la lista de productos cuando se obtienen los datos -->
    <div v-else class="product-list">
      <div v-for="product in products" :key="product.id" class="product-card">
        <img :src="product.image" class="product-image" alt="Product Image">
        <div class="product-details">
          <h3>{{ product.title }}</h3>
          <p class="price">$ {{ product.price }}</p>
          <p>{{ product.description }}</p>
          <p>Category: {{ product.category }}</p>
          <div class="rating">
            Rating: {{ product.rating.rate }} ({{ product.rating.count }} reviews)
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';

export default {
  name: 'ProductosLista',
  setup() {
    const products = ref([]);
    const loading = ref(true); // Variable para mostrar el estado de carga

    const fetchProducts = async () => {
      try {
        const response = await fetch('https://fakestoreapi.com/products');
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        products.value = await response.json();
      } catch (error) {
        console.error('Error fetching products:', error);
      } finally {
        loading.value = false; // Se oculta el mensaje de carga cuando la petición finaliza
      }
    };

    onMounted(fetchProducts);

    return {
      products,
      loading
    };
  }
};
</script>

<style scoped>
.product-list {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}

.product-card {
  width: 300px;
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 5px;
  transition: transform 0.3s ease;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.product-card:hover {
  transform: scale(1.05);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
}

.product-image {
  width: 100%;
  border-radius: 5px;
}

.product-details {
  margin-top: 10px;
}

.price {
  font-weight: bold;
  color: #007bff;
}

.rating {
  margin-top: 5px;
  font-style: italic;
}

.loading {
  text-align: center;
  font-size: 1.5em;
  color: #555;
}

h1 {
  text-align: center;
  margin-bottom: 20px;
  font-size: 2.5em;
  color: #333;
}

.slogan {
  text-align: center;
  margin-bottom: 40px;
  font-size: 1.8em;
  color: #555;
}
</style>
