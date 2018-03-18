<template>
  <div class="container">
    <h1>VUE + WOT API demo App</h1>
    <h3>Source code on <a href="https://github.com/ircykk/vue-wot">@ircykk</a> GitHub | <a href="https://kierkowski.com/world-of-tanks-rest-api-w-vuejs/">blog post</a>.</h3>
    <small>World of Tanks is a trademark of <a href="http://wargaming.net">Wargaming.net</a></small>

    <p>&nbsp;</p>

    <!-- Search form -->
    <form v-on:submit="userId=userId" class="form">
      <div class="form-group mx-sm-3">
        <input v-model="userId" type="text" class="form-control" id="" placeholder="World of Tanks User ID">
      </div>
      <div>
        <small>Some players: <a v-on:click="userId=503811655" href="#">503811655</a></small>
      </div>
    </form>

    <!-- Warning -->
    <div v-if="user===false">
      <div class="alert alert-warning">User not found!</div>
    </div>

    <div v-if="user">

      <hr>

      <h2>{{ user.nickname }} <span v-if="user.clan_id" class="badge badge-default">[{{ user.clan_id }}]</span></h2>

      <p>Last battle: {{ new Date(user.last_battle_time * 1000).toLocaleString() }}</p>

      <div class="row">
        <div class="col-md-3">
          <div class="card">
            <div class="card-block">
              <h4 class="card-title">{{ user.statistics.all.battles.toLocaleString() }}</h4>
            </div>
            <div class="card-footer">
              <small class="text-muted">Battles</small>
            </div>
          </div>
        </div>
        <div class="col-md-3">
          <div class="card">
            <div class="card-block">
              <h4 class="card-title">{{ user.statistics.all.frags.toLocaleString() }}</h4>
            </div>
            <div class="card-footer">
              <small class="text-muted">Frags</small>
            </div>
          </div>
        </div>
        <div class="col-md-3">
          <div class="card">
            <div class="card-block">
              <h4 class="card-title">{{ user.statistics.all.wins.toLocaleString() }}</h4>
            </div>
            <div class="card-footer">
              <small class="text-muted">Wins</small>
            </div>
          </div>
        </div>
        <div class="col-md-3">
          <div class="card">
            <div class="card-block">
              <h4 class="card-title">{{ user.statistics.all.max_xp.toLocaleString() }}</h4>
            </div>
            <div class="card-footer">
              <small class="text-muted">Max. Exp</small>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios'

// Wot API Key
const API_KEY = 'YOUR_API_KEY'

// Wot API URL
const API_URL = 'https://api.worldoftanks.eu/wot/'

export default {
  data () {
    return {
      user: null,
      userId: null
    }
  },
  created () {},
  watch: {
    userId: function () {
      axios
        .get(
          API_URL + `account/info/?application_id=` + API_KEY + `&account_id=` + this.userId
        )
        .then(response => {
          if (typeof response.data.data !== 'undefined' && response.data.data[this.userId]) {
            this.user = response.data.data[this.userId]
          } else {
            this.user = false
          }
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card-title {
  font-size: 40px;
  margin-top: 20px;
}
</style>
