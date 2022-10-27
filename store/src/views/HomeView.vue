<template>

  <div style="display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;">
    <v-card elevation="0" class="my-auto" max-width="400px">
      <v-card-text>
        <v-carousel hide-delimiters height="300">
          <v-carousel-item v-for="(img,i) in images" :key="i">
            <v-img :src="img" contain max-height="300"></v-img>
          </v-carousel-item>
        </v-carousel>
      </v-card-text>
      <v-card-actions class="px-8">
        <v-btn @click="display = 0" color="grey darken-4 white--text" small>BLACK</v-btn>
        <v-btn @click="display = 1" color="grey white--text" small>GREY</v-btn>
        <v-btn @click="display = 2" color="pink lighten-3 white--text" small>PINK</v-btn>
        <v-spacer />
        <v-btn @click="addCart" small>ADD</v-btn>
      </v-card-actions>
      <div v-if="cart.length > 0">
      <v-simple-table dense style="width: 100%" class="px-4">
        <thead>
          <tr>
            <th class="text-left">
              Description
            </th>
            <th class="text-right">
              Quantity
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(product,i) in cart" :key="i">
            <td>{{ product.color }}</td>
            <td class="text-right">
              <input style="text-align:center" v-model="product.qty" min="1" max="5" type="number" />
              <v-btn @click="removeCart(i)" x-small icon>
                <v-icon small>mdi-close</v-icon>
              </v-btn>
            </td>
          </tr>
        </tbody>
      </v-simple-table>
      <v-btn @click="checkout" class="my-2" text dense block>CHECKOUT</v-btn>
    </div>
    </v-card>
    <stripe-checkout ref="checkoutRef" mode="payment"
      pk="pk_test_51LugSHJlyGrOuzyMyptZ0505rGbH8W4RJ5LlBOnBApQc1t4wvjCF9a2dOLruM2rePCjp8AQw9OwG1dwq3Do74HRU00C2kPGc46"
      :line-items="lineItems" :shippingAddressCollection="{allowedCountries: ['US', 'CA']}"
      success-url="https://www.onelifedrift.club" cancel-url="https://www.onelifedrift.club"
      @loading="v => loading = v" />
  </div>

  <!-- <v-container style="max-width: 300px" fill-height>
    <stripe-checkout ref="checkoutRef" mode="payment"
      pk="pk_test_51LugSHJlyGrOuzyMyptZ0505rGbH8W4RJ5LlBOnBApQc1t4wvjCF9a2dOLruM2rePCjp8AQw9OwG1dwq3Do74HRU00C2kPGc46"
      :line-items="lineItems" :shippingAddressCollection="{allowedCountries: ['US', 'CA']}"
      success-url="https://www.onelifedrift.club" cancel-url="https://www.onelifedrift.club"
      @loading="v => loading = v" />
    <v-row>
      <v-card elevation="0">
        <v-card-text>
          <v-carousel hide-delimiters height="320px">
            <v-carousel-item v-for="(img,i) in images" :key="i" :src="img"></v-carousel-item>
          </v-carousel>
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
            <th class="text-right">
              Quantity
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(product,i) in cart" :key="i">
            <td>{{ product.color }}</td>
            <td class="text-right">
              <input style="text-align:center" v-model="product.qty" min="1" max="5" type="number" />
              <v-btn @click="removeCart(i)" x-small icon>
                <v-icon small>mdi-close</v-icon>
              </v-btn>
            </td>
          </tr>
        </tbody>
      </v-simple-table>
      <v-btn @click="checkout" class="my-2" text dense block>CHECKOUT</v-btn>
    </v-row>
  </v-container> -->
</template>

<script>
  import { StripeCheckout } from '@vue-stripe/vue-stripe';
  export default {
    components: {
      StripeCheckout,
    },
    name: 'HomeView',
    data() {
      return {
        loading: false,
        lineItems: [
          {
            price: 'price_1Lv0nqJlyGrOuzyM3bPMpaef', // The id of the one-time price you created in your Stripe dashboard
            quantity: 1,
          },
          {
            price: 'price_1LxFDoJlyGrOuzyM6m9HOaBm', // The id of the one-time price you created in your Stripe dashboard
            quantity: 3,
          },
          {
            price: 'price_1LxFDKJlyGrOuzyMo1saczit', // The id of the one-time price you created in your Stripe dashboard
            quantity: 2,
          },
        ],
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
            imgs: ["https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_51.webp",
              "https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_51.webp",
              "https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_51.webp",
              "https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_51.webp",
              "https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_51.webp"],
            qty: 1,
            price: 'price_1LxFDoJlyGrOuzyM6m9HOaBm'
          },
          {
            color: "grey",
            imgs: ["https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_70.webp",
              "https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_70.webp",
              "https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_70.webp",
              "https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_70.webp",
              "https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_70.webp",
            ],
            qty: 1,
            price: "price_1Lv0nqJlyGrOuzyM3bPMpaef"
          },
          {
            color: "pink",
            imgs: ["https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_01.webp",
              "https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_01.webp",
              "https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_01.webp",
              "https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_01.webp",
              "https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_01.webp"],
            qty: 1,
            price: "price_1LxFDKJlyGrOuzyMo1saczit"
          }
        ],
        cart: []
      }
    },
    computed: {
      productImage() {
        return this.products[this.display].img
      },
      images() {
        return this.products[this.display].imgs
      },
    },
    methods: {
      addCart() {
        if (!this.cart.includes(this.products[this.display]))
          this.cart.push(this.products[this.display])
      },
      removeCart(index) {
        this.cart[index].qty = 1
        this.cart.splice(index, 1)
      },
      checkout() {
        // You will be redirected to Stripe's secure checkout page
        // this.$refs.checkoutRef.redirectToCheckout();
        var myHeaders = new Headers();
        myHeaders.append("Authorization", "Bearer rk_test_51LugSHJlyGrOuzyMFqTc84zqLmxQuao2EhirUwukl0pKosNZSI7OihIGGpV0dQHm8GpF9YgpnwpO6UUZgdMtdklV00TX1AriHa");
        myHeaders.append("Content-Type", "application/x-www-form-urlencoded");

        var urlencoded = new URLSearchParams();
        urlencoded.append("success_url", "https://example.com/success");
        urlencoded.append("cancel_url", "https://example.com/cancel");

        this.cart.forEach((element, i) => {
          urlencoded.append(`line_items[${i}][price]`, element.price);
          urlencoded.append(`line_items[${i}][quantity]`, element.qty);
        });

        // urlencoded.append("line_items[0][price]", "price_1LxFDKJlyGrOuzyMo1saczit");
        // urlencoded.append("line_items[0][quantity]", "2");
        urlencoded.append("mode", "payment");
        urlencoded.append("allow_promotion_codes", "true");
        urlencoded.append("shipping_address_collection[allowed_countries][0]", "US");

        var requestOptions = {
          method: 'POST',
          headers: myHeaders,
          body: urlencoded,
          redirect: 'follow'
        };

        fetch("https://api.stripe.com/v1/checkout/sessions", requestOptions)
          .then(response => response.text())
          .then(result => console.log(result))
          .catch(error => console.log('error', error));
      },
    }
  }
</script>