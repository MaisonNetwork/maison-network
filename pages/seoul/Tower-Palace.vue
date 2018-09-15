<template>
  <v-layout :class="{'pa-0': $vuetify.breakpoint.xsAndDown, 'pa-5': $vuetify.breakpoint.smAndUp}">
      <v-layout row wrap>
        <v-flex xs12 md6>
          <v-carousel>
            <v-carousel-item
            v-for="(item,i) in photos"
            :key="i"
            :src="item.src"
            ></v-carousel-item>
          </v-carousel>
        </v-flex>
        <v-flex xs12 md6>
          <v-layout class="pa-3" column>
            <v-layout row wrap>
              <h1>6 Bedroom Penthouse</h1>
              <v-chip class="ml-3 hidden-sm-and-down">For Rent</v-chip>
            </v-layout>
            <p class="subheading grey--text">Gangnam, Seoul</p>
            <div>
            </div>
            <h1>$4000 p/m</h1>
            <p class="subheading grey--text">($100 per sq m)</p>
            <div>
              <v-btn outline large round color="green" @click="dialog = true; init();">Rent</v-btn>
            </div>  
          </v-layout>
        </v-flex>
      </v-layout>

    <v-dialog v-model="dialog" width="500">
      <v-card style="border-radius: 20px;">
        <v-card-title class="headline green lighten-2" primary-title>
          6 Bedroom Penthouse
        </v-card-title>
        <v-card-text class="grey--text">
          Gangnam, Seoul
        </v-card-text>
        <v-form class="px-4" ref="form" v-model="valid" lazy-validation>
          <v-text-field
            v-model="name"
            :rules="nameRules"
            :counter="10"
            label="Name"
            required
          ></v-text-field>
          <v-text-field
            v-model="email"
            :rules="emailRules"
            label="E-mail"
            required
          ></v-text-field>
          <v-select
            v-model="select"
            :items="items"
            :rules="[v => !!v || 'Ownership plan is required']"
            label="Ownership plan"
            required
          ></v-select>
          <v-text-field
            value="$10,000"
            label="deposit"
            readonly
          ></v-text-field>
        </v-form>
        <v-divider></v-divider>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" flat @click="donate(); dialog = false">
            Confirm
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-layout>
</template>

<script>
export default {
data() {
  var network = "Mainnet";

  return {
    dialog: false,
    valid: true,
    name: '',
    active: null,
    nameRules: [
      v => !!v || 'Name is required',
      v => (v && v.length <= 10) || 'Name must be less than 10 characters'
    ],
    email: '',
    emailRules: [
      v => !!v || 'E-mail is required',
      v => /.+@.+/.test(v) || 'E-mail must be valid'
    ],
    select: null,
    items: [
      'Asset Token',
      'Index Token'
    ],
    photos: [
        {
          src: 'http://images.skyscrapercenter.com/building/towerpalacethreetowerg_lookup_mg.jpg'
        },
        {
          src: 'http://post.phinf.naver.net/MjAxNzExMzBfMjc3/MDAxNTEyMDI0ODc3MDYx.1dkl_C3cI9QDPoUPjrbCFiYnsnXIXXGYfJH9nVs7fmYg.YZDpB75uh7RstRqE2ng9YG_xiP1GDYRH-o4Gxdwn4swg.JPEG/ITASs696SY2NdWBH15AEajk58W5w.jpg'
        }
      ],
    checkbox: false,
    init: function() {
      if (typeof web3 !== 'undefined') {
        web3 = new Web3(web3.currentProvider);
        web3.eth.getAccounts(function(error, accounts) {
          if (error) { console.log(error);}
          else if (accounts.length == 0) {
            alert("*Please unlock Metamask in order to donate");
            this.dialog = false;
          }
        });
      } else {
        alert("If you wish to pay with crypto, please install a web3 provider like Metamask: https://metamask.io/");
        this.dialog = false;
      }
    },
    donate: function() {
      web3.eth.getAccounts(function(error, accounts) {
        if (error) { console.log(error);
        } else {
          var account = accounts[0];
          var amount = 10;
          var charity = "0x4209a2fc29f8c9337e32823a1c773afd6aa5ce42";
          web3.eth.sendTransaction({from: account, to: charity, value:web3.toWei(amount, "ether"), gasPrice: web3.toWei(5,'gwei')}, function(err, transactionHash){
            if (!err)
              alert("Thanks for your donation. TX hash: " + transactionHash.substring(0,8) + "...");
          });
        }
      });
    },
  }
}
}

</script>
