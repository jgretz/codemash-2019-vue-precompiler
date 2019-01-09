<template>
  <div class="cart">
    <table class="table thead-light tabled-striped">
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
          <th>Quantity</th>
          <th>Total</th>
          <th>Edit</th>
          <th>Is Healthy</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(line, i) in cart" v-bind:key="i">
          <td>{{line.name}}</td>
          <td>{{line.price | currency}}</td>
          <td>{{line.quantity}}</td>
          <td>{{line.price * line.quantity | currency}}</td>
          <td nowrap>
            <button class="btn btn-info btn-sm" @click="line.edit = !line.edit">Edit</button>
            <button class="btn btn-danger btn-sm" @click="removeLine(line)">Delete</button>
          </td>
          <td v-if="line.isHealthy">
            <img src="https://vignette.wikia.nocookie.net/fossils-archeology/images/c/c3/Kermit-the-frog-yay-gif-526028.jpg/revision/latest?cb=20151106043631" />
          </td>
          <td v-else>
            <img src="https://cdn.psychologytoday.com/sites/default/files/styles/image-article_inline_full/public/field_blog_entry_images/Sadness_standard2.jpg?itok=FWzmW4cQ" />
          </td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <td>Totals:</td>
          <td></td>
          <td></td>
          <td>{{cartTotal | currency}}</td>
          <td></td>
          <td></td>
        </tr>
        <tr />
        <AddItem :on-save="addItem" />
      </tfoot>
    </table>
  </div>
</template>

<script>
import AddItem from './AddItem.vue';
import cartData from '../constants/data';

export default {
  name: 'Cart',
  components: {
    AddItem,
  },

  data: () => ({
    cart: cartData,
  }),
  computed: {
    cartTotal: ({cart}) => {
      return cart.reduce((total, line) => total += line.quantity * line.price, 0);
    },
  },
  filters: {
    currency: (value) => {
      return value ? `$${parseFloat(value).toFixed(2)}` : '';
    }
  },

  methods: {
    addItem: function(item) {
      this.cart.push(item);
    },

    removeLine: function(line) {
      this.cart = this.cart.filter(x => x !== line);
    },
  }
}
</script>

