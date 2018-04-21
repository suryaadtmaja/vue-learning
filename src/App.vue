<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <h1>Http</h1>
          <div class="form-group">
            <label>Username</label>
            <input type="text" class="form-group" v-model="user.username">
          </div>
          <div class="form-group">
            <label>Mail</label>
            <input type="text" class="form-group" v-model="user.email">
          </div>
          <button class="btn btn-primary" @click="submit">
            Submit
          </button>
          <hr>
          <button class="btn btn-primary" @click="fetchData">
            Get Data
          </button>
          <br>
          <br>
          <ul class="list-group">
            <li class="list-group-item" v-for="u in users">
              {{ u.username }} - {{ u.email }}
            </li>
          </ul>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    data() {
      return {
        user: {
          username: '',
          email: ''
        },
        users: []
      };
    }, 
    methods: {
      submit() {
        this.$http.post('https://vuejs-e530a.firebaseio.com/data.json', this.user)
        .then(function (response) {
          console.log(response);
        })
        .catch(function (error) {
          console.log(error);
        });
      },
      fetchData() {
        this.$http.get('https://vuejs-e530a.firebaseio.com/data.json')
        .then(function(data) {
          return data.json();
        }).then (function(data){
          var userAray = [];
          for (let key in data){
            userAray.push(data[key]);
          }
          this.users = userAray;
        })
      }
    }
  }
</script>

<style>
</style>
