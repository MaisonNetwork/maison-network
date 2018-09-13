<template>
  <div>
    <v-layout column align-center justify-space-between>
      <v-card flat color="transparent">
        <v-layout class="mt-3" row>
          <v-card flat color="transparent" width="100px">
            <div
            v-text="`$${price[0]}`"
            class="mt-3"
            hide-details
            single-line
            type="number"
            flat
            ></div>
          </v-card>
          <v-card flat color="transparent" width="500px">
            <v-range-slider
            v-model="price"
            :max="5000"
            :min="1500"
            :step="100"
            flat
            ></v-range-slider>
          </v-card>
          <v-card flat color="transparent" width="100px">
            <div
            v-text="`$${price[1]}`"
            class="mt-3 ml-5"
            hide-details
            single-line
            type="number"
            solo
            flat
            ></div>
          </v-card>
        </v-layout>
      </v-card>
      <v-card flat color="transparent" width="400">
        <div>
        Equity accrued after five years: between <strong>{{price[0]/1000}}%</strong> and <strong>{{price[1]/1000}}%</strong>
        </div>
      </v-card>
      <v-flex xs12 sm6>
        <v-card width="1000" flat color="transparent">
          <v-container fluid grid-list-md>
            <v-layout row wrap>
              <v-flex v-for="card in filteredCards" v-bind="{ [`xs${card.flex}`]: true }" :key="card.title">
                <v-card nuxt :to="card.link">
                  <v-img :src="card.src" height="200px">
                    <v-container fill-height fluid pa-2>
                      <v-layout fill-height>
                        <v-flex xs12 align-end flexbox>
                          <span class="headline white--text" v-text="card.title"></span>
                        </v-flex>
                      </v-layout>
                    </v-container>
                  </v-img>
                  <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn icon>
                      <v-icon>favorite</v-icon>
                    </v-btn>
                    <v-btn icon>
                      <v-icon>bookmark</v-icon>
                    </v-btn>
                    <v-btn icon>
                      <v-icon>share</v-icon>
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-flex>
            </v-layout>
          </v-container>
        </v-card>
      </v-flex>
    </v-layout>
  </div>
</template>


<script>
export default {
   data() {
     return {
    cards: [
      { title: 'Tower Palace A', src: 'http://post.phinf.naver.net/MjAxNzExMzBfMjc3/MDAxNTEyMDI0ODc3MDYx.1dkl_C3cI9QDPoUPjrbCFiYnsnXIXXGYfJH9nVs7fmYg.YZDpB75uh7RstRqE2ng9YG_xiP1GDYRH-o4Gxdwn4swg.JPEG/ITASs696SY2NdWBH15AEajk58W5w.jpg', flex: 6, link: "/Seoul/Tower-Palace", price: "4900" },
      { title: 'Bonham avenue', src: 'https://colorlib.com/preview/theme/tough/images/bg_1.jpg', flex: 6, link: "/seoul/Tower-Palace", price: "3500" },
      { title: 'Hill 36', src: 'https://colorlib.com/preview/theme/tough/images/image_3.jpg', flex: 6, link: "/seoul/Tower-Palace", price: "1600" },
      { title: 'Bond Row', src: 'https://i.imgur.com/PV6UjK7.jpg', flex: 6, link: "/seoul/Tower-Palace", price: "2500" },
      { title: 'Clapham Junction', src: 'https://i.imgur.com/IzbtiNU.jpg', flex: 6, link: "/seoul/Tower-Palace", price: "3500" },
      { title: 'Cotswold', src: 'http://zaghlulalnaggar.com/wp-content/uploads/2017/11/wunderbar-maison-kayser-pickle-margiela-http-www-maisondupuy-com-premiere-maisonette-sneakers-harlem-louis-marie-kitsune-menu-hugo-du-chocolat-francis-de.jpg', flex: 6, link: "/Seoul/Tower-Palace", price: "4500" }
    ],
    price: [1500, 5000]
   }
  },
  computed: {
    filteredCards() {
      return this.cards.filter(card => {return card.price < this.price[1] && card.price > this.price[0]})
    }
  }
}
</script>
