<template>
  <tr>
    <td>
      <input type="text" class="form-control" name="name" id="" v-model="newItem.name" />
    </td>
    <td>
      <div class="input-group">
        <div class="input-group-prepend">
          <span class="input-group-text">$</span>
        </div>
        <input class="form-control" type="text" name="price" id="" v-model="newItem.price">
      </div>
    </td>
    <td>
      <div class="input-group">
        <input class="form-control" type="text" name="quantity" id="" v-model="newItem.quantity">
        <div class="input-group-append">
          <button class="btn btn-secondary" @click="newItem.quantity--">-</button>
          <button class="btn btn-secondary" @click="newItem.quantity++">+</button>
        </div>
      </div>
    </td>
    <td>
      <input type="checkbox" class="form-control" name="price" id="" title="Be Honest" v-model="newItem.isHealthy" />
    </td>
    <td></td>
    <td>
      <input type="submit" class="btn btn-info" @click="addItemToCart" value="Add To Cart">
    </td>
    <td></td>
  </tr>
</template>

<script>
export default {
  name: 'AddItem',
  props: {
    onSave: [Function],
  },

  data: () => ({
    newItem: {
      name: '',
      quantity: 0,
      price: 0,
      isHealthy: false,
      edit: false
    }
  }),

  methods: {
    addItemToCart: function () {
      const {newItem, onSave, resetForm} = this;
      
      onSave(newItem);
      resetForm();
    },
    resetForm: function () {
      this.newItem = {
        name: '',
        quantity: 0,
        price: 0,
        isHealthy: false
      };
    },
  },
}
</script>

