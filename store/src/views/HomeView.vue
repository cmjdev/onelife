<template>

  <v-container fill-height style="max-width: 1000px">
    <v-row>
      <v-col cols="0" sm="6">
        <v-img contain height="100%" :src="require('../assets/skull.png')"></v-img>
      </v-col>
      <v-col cols="12" sm="6">
        <v-img contain height="100%" src="https://cdn.blankstyle.com/files/imagecache/product/p_images/8184/1501_70.webp">
          <v-container fill-height fluid>
            <v-row no-gutters class="fill-height">
              <v-col cols="10" align-self="end">
                <v-btn class="mx-1 grey darken-3 white--text">BLACK</v-btn>
                <v-btn class="mx-1 grey white--text">GREY</v-btn>
                <v-btn class="mx-1 pink lighten-2 white--text">PINK</v-btn>
              </v-col>
              <v-col cols="2" align-self="end">
                <v-spacer />
                <v-btn>BUY</v-btn>
              </v-col>
            </v-row>
          </v-container>
        </v-img>
        
      </v-col>
    </v-row>
    
    <v-row v-if="false" class="fill-height">
      <v-col>
      <v-card elevation="0">
        <v-card-title>Shopping Cart</v-card-title>
        <v-card-text>
          <v-data-table :headers="headers" :items="desserts" hide-default-footer></v-data-table>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn small>BUY</v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
    </v-row>
  </v-container>

</template>

<script>

  export default {
    name: 'HomeView',
    data() {
      return {
      desserts: [
          {
            name: 'Frozen Yogurt',
            calories: 159,
            fat: 6.0,
            carbs: 24,
            protein: 4.0,
            iron: '1%',
          },
          {
            name: 'Ice cream sandwich',
            calories: 237,
            fat: 9.0,
            carbs: 37,
            protein: 4.3,
            iron: '1%',
          },
          {
            name: 'Eclair',
            calories: 262,
            fat: 16.0,
            carbs: 23,
            protein: 6.0,
            iron: '7%',
          },
          {
            name: 'Cupcake',
            calories: 305,
            fat: 3.7,
            carbs: 67,
            protein: 4.3,
            iron: '8%',
          },
          {
            name: 'Gingerbread',
            calories: 356,
            fat: 16.0,
            carbs: 49,
            protein: 3.9,
            iron: '16%',
          },
          {
            name: 'Jelly bean',
            calories: 375,
            fat: 0.0,
            carbs: 94,
            protein: 0.0,
            iron: '0%',
          },
          {
            name: 'Lollipop',
            calories: 392,
            fat: 0.2,
            carbs: 98,
            protein: 0,
            iron: '2%',
          },
          {
            name: 'Honeycomb',
            calories: 408,
            fat: 3.2,
            carbs: 87,
            protein: 6.5,
            iron: '45%',
          },
          {
            name: 'Donut',
            calories: 452,
            fat: 25.0,
            carbs: 51,
            protein: 4.9,
            iron: '22%',
          },
          {
            name: 'KitKat',
            calories: 518,
            fat: 26.0,
            carbs: 65,
            protein: 7,
            iron: '6%',
          },
        ],
    }
  },
  computed: {
      headers () {
        return [
          {
            text: 'Dessert (100g serving)',
            align: 'start',
            sortable: false,
            value: 'name',
          },
          {
            text: 'Calories',
            value: 'calories',
          },
          { text: 'Fat (g)', value: 'fat' },
          { text: 'Carbs (g)', value: 'carbs' },
          { text: 'Protein (g)', value: 'protein' },
          { text: 'Iron (%)', value: 'iron' },
        ]
      },
    }
  }
</script>