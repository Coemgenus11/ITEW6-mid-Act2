<template>
    <main id="products-page">


            <div class="container">
                <h1 class="page-title">Product List</h1>
                <p class="page-description">Browse our products below.</p>
                <div class="product-list">
                    <transition-group name="slide" tag="div">
                        <div v-for="product in products" :key="product.id" class="product-item">
                            <div class="product-details">
                                <h2>{{ product.name }}</h2>
                                <p class="description">{{ product.description }}</p>
                                <p class="price">{{ formatCurrency(product.price) }}</p>
                            </div>
                            <div class="product-actions">
                                <button @click="editProduct(product)" class="action-button edit-button">Edit</button>
                                <button @click="deleteProduct(product.id)" class="action-button delete-button">Delete</button>
                            </div>
                        </div>
                    </transition-group>
                </div>
            </div>
        
    </main>
  </template>
  
  <script>
  export default {
    props: ['products'],
    methods: {
      editProduct(product) {
        this.$emit('edit', product);
      },
      deleteProduct(productId) {
        this.$emit('delete', productId);
      },
      formatCurrency(price) {
        return new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(price);
      }
    }
  };
</script>
  
<style scoped>
 /* Add animation */
/* CSS for Slide Transition */
.slide-item {
  transition: transform 1s ease-out;
}
.slide-enter-active{
  transition: transform 1s ease-out;
}
.slide-enter /* .slide-leave-active in <2.1.8 */ {
  transform: translateY(8);
}
.slide-enter-to /* .slide-enter-active in <2.1.8 */ {
  transform: translateY(100%);
}

.slide-leave-active {
  transition: transform 0.5s ease;
}

.slide-leave-to {
  transform: translateY(100%);
}
  
  .container {
    margin: 0 auto;
    padding: 40px;
    background-color: #fff;
    border-radius: 8px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  }
  
  .page-title {
    font-size: 32px;
    color: #333;
    margin-bottom: 20px;
  }
  
  .page-description {
    font-size: 18px;
    color: #666;
    margin-bottom: 30px;
  }
  
  .product-list {
    display: grid;
    gap: 20px;

  }
  
  .product-item {
    display: grid;
    grid-template-columns: 2fr 1fr;
    gap: 20px;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 4px rgba(0, 0, 0, 0.5);
    background-color: rgb(255, 234, 189);
    transition: transform 0.2s ease;
  }
  
  .product-item:hover {
    background-color: rgb(188, 173, 173);
    color: chartreuse;
    box-shadow: 0 0 4px rgba(0, 0, 0, 1);
  }
  
  .product-details {
    display: flex;
    flex-direction: column;
  }
  
  .description {
    color: #555;
    margin-bottom: 10px;
  }
  
  .price {
    font-weight: bold;
    color: #007bff;
  }
  
  .product-actions {
    display: flex;
    align-items: center;
  }
  
  .action-button {
    padding: 10px 15px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 16px;
  }
  
  .edit-button {
    background-color: #007bff;
    color: #fff;
  }
  
  .delete-button {
    background-color: #dc3545;
    color: #fff;
  }
  
  .action-button:hover {
    opacity: 0.8;
  }
  </style>
  