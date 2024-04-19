<template>
  <div class="add-product">
    <h2>Add Product</h2>
    <form @submit.prevent="addProduct" class="form">
      <div class="form-group">
        <label for="name">Product Name</label>
        <input id="name" v-model="newProduct.name" placeholder="Enter product name" required>
      </div>
      <div class="form-group">
        <label for="description">Description</label>
        <textarea id="description" v-model="newProduct.description" placeholder="Enter product description" required></textarea>
      </div>
      <div class="form-group">
        <label for="price">Price</label>
        <input id="price" v-model.number="newProduct.price" oninput="this.value = this.value.replace(/[^0-9]/g, '')" type="text" placeholder="Enter product price" required>
      </div>
      <button type="submit">Add</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newProduct: {
        name: '',
        description: '',
        price: ''
      }
    };
  },
  methods: {
    addProduct() {
      this.$emit('add', this.newProduct);
      this.newProduct = { name: '', description: '', price: '' };
    }
  }
};
</script>

<style scoped>
.add-product {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
}

h2 {
  text-align: center;
  margin-bottom: 20px;
  color: #333;
}

.form {
  display: grid;
  gap: 15px;
}

.form-group {
  display: grid;
  gap: 8px;
}

label {
  font-weight: bold;
}

input,
textarea {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

button {
  width: 100%;
  padding: 12px;
  border: none;
  border-radius: 4px;
  background-color: #007bff;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>
