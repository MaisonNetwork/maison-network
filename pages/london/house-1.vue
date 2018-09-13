<template>
  <v-layout column align-center justify-space-between>
    <v-card flat color="transparent" class="mt-3" width="1000">
      <v-layout row justify-space-between>
        <v-layout column>
          <v-img src="https://cdn.vuetifyjs.com/images/cards/house.jpg" width="400px" height="400px"/>

        </v-layout>

        <v-layout class="pl-3 pt-3" column>
          <h2>3 Bed Maisonette For Rent</h2>
          <p class="subheading grey--text">Webber Street, London SE1</p>
          <h1>$2000 p/m</h1>
          <p class="subheading grey--text">($100 per sq m)</p>
            <v-card flat color="transparent" width=50px>
              <v-btn round color="green" @click="dialog = true">Rent</v-btn>
            </v-card>
        </v-layout>
      </v-layout>
    </v-card>
    <a class="mt-2 grey--text" target="_blank" href="https://www.zoopla.com">View on Zoopla</a>
    <v-card flat color="transparent" class="mt-3" width="400">
      <v-tabs v-model="active" color="cyan" dark slider-color="black">
        <v-tab ripple>
          Floorplan
        </v-tab>
        <v-tab-item>
          <v-card flat>
          </v-card>
        </v-tab-item>
        <v-tab ripple>
          Floorplan
        </v-tab>
        <v-tab-item>
          <v-card flat>
          </v-card>
        </v-tab-item>
      </v-tabs>
      <div class="text-xs-center mt-3">
        <v-btn @click="next">next tab</v-btn>
      </div>
    </v-card>
    <v-dialog v-model="dialog" width="500">
      <v-card style="border-radius: 20px;">
        <v-card-title class="headline green lighten-2" primary-title>
          3 Bed Maisonette
        </v-card-title>
        <v-card-text class="grey--text">
          Webber Street, London SE1
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
            value="$1000"
            label="deposit"
            readonly
          ></v-text-field>
        </v-form>
        <v-divider></v-divider>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" flat @click="dialog = false">
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
    checkbox: false
  }},
}

</script>
