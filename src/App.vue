<template>
  <div class="crud-container">
    <h1>CRUD Application</h1>
    <form @submit.prevent="addItem" class="crud-form">
      <input v-model="newItem" placeholder="Add new item" />
      <button type="submit">Add</button>
    </form>
    <ul class="crud-list">
      <li v-for="(item, index) in items" :key="index" class="crud-item">
        <div v-if="!item.editing">
          {{ item.name }}
          <button @click="editItem(index)">Edit</button>
          <button @click="deleteItem(index)">Delete</button>
        </div>
        <div v-else>
          <input v-model="item.newName" />
          <button @click="updateItem(index)">Update</button>
          <button @click="cancelEdit(index)">Cancel</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newItem: '',
      items: []
    }
  },
  methods: {
    // Add new item to the list
    addItem() {
      if (this.newItem.trim()) {
        this.items.push({ name: this.newItem.trim(), newName: this.newItem.trim(), editing: false })
        this.newItem = ''
      }
    },
    // Enable edit mode for the item
    editItem(index) {
      this.items[index].editing = true
    },
    // Update the item and disable edit mode
    updateItem(index) {
      if (this.items[index].newName.trim()) {
        this.items[index].name = this.items[index].newName.trim()
        this.items[index].editing = false
      }
    },
    // Cancel the edit mode
    cancelEdit(index) {
      this.items[index].editing = false
      this.items[index].newName = this.items[index].name
    },
    // Delete the item from the list
    deleteItem(index) {
      this.items.splice(index, 1)
    }
  }
}
</script>

<style scoped>
.crud-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
}
.crud-form {
  display: flex;
  margin-bottom: 20px;
}
.crud-form input {
  flex: 1;
  padding: 10px;
  margin-right: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.crud-form button {
  padding: 10px 20px;
  border: none;
  background-color: #42b983;
  color: white;
  cursor: pointer;
  border-radius: 4px;
}
.crud-form button:hover {
  background-color: #358a65;
}
.crud-list {
  list-style: none;
  padding: 0;
}
.crud-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 0;
  border-bottom: 1px solid #ccc;
}
.crud-item div {
  display: flex;
  align-items: center;
}
.crud-item input {
  margin-right: 10px;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.crud-item button {
  margin-left: 10px;
  padding: 5px 10px;
  border: none;
  cursor: pointer;
  border-radius: 4px;
}
.crud-item button:hover {
  background-color: #ddd;
}
</style>
