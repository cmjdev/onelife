<template>
  <v-container style="max-width: 300px" fill-height>
    <v-row>
      <v-card elevation="0">
        <v-card-text>
          <v-img contain max-height="300px" :src="products[display].img"></v-img>

        </v-card-text>
        <v-card-actions class="py-4">
          <v-btn @click="display = 0" color="grey darken-4 white--text" small>BLACK</v-btn>
          <v-btn @click="display = 1" color="grey white--text" small>GREY</v-btn>
          <v-btn @click="display = 2" color="pink lighten-3 white--text" small>PINK</v-btn>
          <v-spacer />
          <v-btn @click="addCart" small>ADD</v-btn>
        </v-card-actions>
      </v-card>
      <v-simple-table dense style="width: 100%">
        <thead>
          <tr>
            <th class="text-left">
              Description
            </th>
            <th class="text-center">
              Quantity
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="product in cart" :key="product.img">
            <td>{{ product.color }}</td>
            <td class="text-center">
              <input v-model="product.qty" min="1" max="5" type="number" />
            </td>
          </tr>
        </tbody>
      </v-simple-table>
      <v-btn class="my-2" text dense block>CHECKOUT</v-btn>
    </v-row>
  </v-container>
</template>

<script>

  export default {
    name: 'HomeView',
    data() {
      return {
        display: 0,
        headers: [
          {
            text: "color",
            value: "value"
          }
        ],
        products: [
          {
            color: "black",
            img: "https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_51.webp",
            qty: 1
          },
          {
            color: "grey",
            img: "https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_70.webp",
            qty: 1
          },
          {
            color: "pink",
            img: "https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_01.webp",
            qty: 1
          }
        ],
        cart: []
      }
    },
    computed: {
      productImage() {
        return this.products[this.display].img
      },
    },
    methods: {
      addCart() {
        if (!this.cart.includes(this.products[this.display]))
          this.cart.push(this.products[this.display])
      }
    }
  }
</script>