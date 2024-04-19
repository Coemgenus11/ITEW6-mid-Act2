<template>
    <main id="manage-page">
      
      <div>
        <AddProduct @add="addProduct" />
        <EditProduct v-if="editingProduct" :product="editingProduct" @update="updateProduct" />
        <ProductListView :products="products" @edit="showEditForm" @delete="deleteProduct" />
      </div>
    </main>
  </template>
  
  <script>
  import { ref } from 'vue';
  import ProductListView from './ProductsListView.vue'; // Import the ProductListView component
  import AddProduct from '../components/AddProduct.vue';
  import EditProduct from '../components/EditProduct.vue';
  
  export default {
    components: {
      ProductListView,
      AddProduct,
      EditProduct
    },
    setup() {
      const products = ref([
        { id: 1, name: 'Product 1', description: 'Description 1', price: 10 },
        { id: 2, name: 'Product 2', description: 'Description 2', price: 20 }
      ]);
      const editingProduct = ref(null);
  
      const addProduct = (newProduct) => {
        products.value.push({ ...newProduct, id: products.value.length + 1 });
        // Add animation after successful addition
      };
  
      const showEditForm = (product) => {
        editingProduct.value = { ...product };
      };
  
      const updateProduct = (editedProduct) => {
        const index = products.value.findIndex(p => p.id === editedProduct.id);
        if (index !== -1) {
          products.value[index] = editedProduct;
          // Add animation after successful update
          editingProduct.value = null;
        }
      };
  
      const deleteProduct = (productId) => {
        const index = products.value.findIndex(p => p.id === productId);
        if (index !== -1) {
          products.value.splice(index, 1);
          // Add animation after successful deletion
        }
      };
  
      return { products, editingProduct, addProduct, showEditForm, updateProduct, deleteProduct };
    }
  };
  </script>