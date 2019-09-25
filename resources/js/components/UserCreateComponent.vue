<template>
  <div>
    <h1>Create A User</h1>
    <form @submit.prevent="addUser">
      <div class="row">
        <div class="col-md-6">
          <div class="form-group">
            <label>Name:</label>
            <input type="text" class="form-control" v-model="user.name">
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-md-6">
          <div class="form-group">
            <label>Email:</label>
            <input type="text" class="form-control" v-model="user.email">
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-md-6">
          <div class="form-group">
            <label>Password:</label>
            <input type="text" class="form-control" v-model="user.password">
          </div>
        </div>
      </div>
      <br />
      <div class="form-group">
        <button class="btn btn-primary">Create</button>
      </div>
    </form>
  </div>
</template>

<script>
    export default {
        data(){
        return {
          user:{}
        }
    },
    methods: {
      addUser(){
        //console.log(this.user);
        let uri = 'http://localhost:8000/api/user/create';
        this.axios.post(uri, this.user).then((response) => {
            this.$router.push({name: 'users'});
        });
      }
    }
  }
</script>