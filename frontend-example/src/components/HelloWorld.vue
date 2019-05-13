<template>
  <div>
  <v-container>
    <v-layout
      text-xs-center
      wrap
    >

 <v-flex xs12 sm6 offset-sm3>
      <v-card>
        <v-card-text>
              <v-form ref="form"><v-layout>
                <v-flex x10 >
          <v-text-field
            v-model="url"
            label="Link to shouten"
          ></v-text-field></v-flex><v-flex x2 class="pt-3">

          <v-btn flat color="blue" @click="getshouten(url)" >Go on!</v-btn></v-flex></v-layout>
        </v-form>
        </v-card-text>
                <v-card-title primary-title>
          <div>
            <div v-if="url" >Url: {{ url }}</div>
          </div>
        </v-card-title>
        <v-card-title primary-title>
          <div>
            <div v-if="shout" >id: {{ shout }}</div>
          </div>
        </v-card-title>
        <v-card-actions>
          <v-btn flat color="orange" @click="restart()">Clear</v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
    </v-layout>
  </v-container>
</div>
</template>

<script>
import axios from 'axios';

export default {
  methods: {
    restart() {
      this.url = '';
    },
    getshouten() {
      axios.post(this.shoutenURL)
        .then((response) => {
          this.shout = response;
        });
    },
  },
  data: () => ({
    apishouten: 'http://shoutlink.herokuapp.com/api/create?url=',
    apiopen: 'http://shoutlink.herokuapp.com/api/open',
    url: '',
    shout: '',
  }),
  computed:
    {
      shoutenURL() {
        return this.apishouten.concat(this.url);
      },
      openURL() {
        return this.concat('/', this.shout);
      },
    },
};
</script>

<style>

</style>
