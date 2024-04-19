<template>
  <div class="edit-product-overlay">
    <div class="edit-product">
      <h2>Edit Product</h2>
      <form @submit.prevent="updateProduct" class="form">
        <div class="form-group">
          <label for="name">Name</label>
          <input id="name" v-model="editedProduct.name" placeholder="Enter product name" required>
        </div>
        <div class="form-group">
          <label for="description">Description</label>
          <textarea id="description" v-model="editedProduct.description" placeholder="Enter product description" required></textarea>
        </div>
        <div class="form-group">
          <label for="price">Price</label>
          <input id="price" v-model.number="editedProduct.price" type="number" placeholder="Enter product price" required>
        </div>
        <button type="submit">Update</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  props: ['product'],
  data() {
    return {
      editedProduct: { ...this.product }
    };
  },
  methods: {
    updateProduct() {
      this.$emit('update', this.editedProduct);
    }
  }
};
</script>

<style scoped>

.edit-product-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.5); /* Semi-transparent overlay */
  
}

.edit-product {
  max-width: 400px;
  width: 100%;
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
