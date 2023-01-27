<template>
  <div>
    <form @submit.prevent="addItem">
      <input v-model="newItem" placeholder="Add item to list">
      <button type="submit">Add</button>
    </form>
    <ul>
      <li v-for="item in items" :key="item">
        <input type="checkbox" v-model="item.checked" @click="checkItem(item)"/>
        {{ item.text }}
      </li>
    </ul>
    <button @click="deleteCheckedItems">Delete Checked Items</button>
    <h2>Checked Items</h2>
    <ul>
      <li v-for="item in checkedItems" :key="item.text">{{ item.text }}</li>
    </ul>
    <h2>Deleted Items</h2>
    <ul>
      <li v-for="item in deletedItems" :key="item.text">{{ item.text }}</li>
    </ul>
  </div>
</template>
<script>
export default {
  data() {
    return {
      newItem: '',
      items: [],
      checkedItems: [],
      deletedItems: []
    }
  },
  methods: {
    addItem() {
      this.items.push({ text: this.newItem, checked: false });
      this.newItem = '';
    },
    checkItem(item) {
      if (item.checked) {
        this.checkedItems.push(item);
      } else {
        this.checkedItems = this.checkedItems.filter(i => i !== item);
      }
    },
    deleteCheckedItems() {
      this.deletedItems = [...this.deletedItems, ...this.checkedItems];
      this.items = this.items.filter(item => !item.checked);
      this.checkedItems = []
    }
  }
}
</script>
