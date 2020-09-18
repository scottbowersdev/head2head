<template>
  <q-page class="fullscreen q-pa-xl vertical-middle">

    <div class="row q-mb-xl justify-center">
      <div class="col-12 text-center">
      <img
        src="../assets/logo.png"
        spinner-color="white"
        style="width: 400px;"
        ratio="1"
        transition="fade"
      />
      </div>
      <div class="col-12 text-center">
      <h5 style="margin-top: 10px;">Head to head football comparison</h5>
      </div>
    </div>

    <div class="row vertical-middle form q-mb-xl">
      <div class="col-5">
        <q-input
          square
          color="primary"
          bg-color="white"
          filled
          :min-input-length="4"
          v-model="team1"
          v-on:keyup="getTeam"
          label="Your Team"
        >
          <template v-slot:no-option>
          <q-item>
            <q-item-section class="text-grey">
              Start typing your team
            </q-item-section>
          </q-item>
        </template>
        </q-input>
      </div>
      <div class="col-2 text-center vs-text">
        <h1>VS</h1>
      </div>
      <div class="col-5">
        <q-select use-input square color="primary" bg-color="white" filled v-model="team2" label="Other Team" />
      </div>
    </div>
    <div class="row vertical-middle form">
      <div class="col-12 text-center">
        <q-btn round color="white" icon="sports_soccer" size="1.6rem" unelevated text-color="primary" />
      </div>
    </div>
    <div>{{ apiResponse }}</div>
  </q-page>
</template>

<script>
import axios from 'axios'
export default {
  name: 'PageIndex',
  data () {
    return {
      team1: '',
      team2: '',
      apiResponse: ''
    }
  },
  methods: {
    getTeam: function () {
      var teamName = this.team1
      var teamLength = teamName.length
      console.log(teamName)

      if (teamLength > 4) {
        axios.get('https://api.coindesk.com/v1/bpi/currentprice.json')
          .then(response => {
            (this.apiResponse = response)
          })
          .catch(e => {
            this.errors.push(e)
          })
      }
    }
  }
}
</script>

<style lang="sass">
  .vs-text
    height: 56px
    line-height: 56px
    margin-top: -10px
    h1
      margin: 0
      padding: 0
      font-size:
</style>
