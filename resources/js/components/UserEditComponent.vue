<template>
  <div>
    <h1>Edit User</h1>
    <form @submit.prevent="updateUser">
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
                    <input type="text" class="form-control" v-model="user.password" placeholder="********">
                </div>
            </div>
        </div>
        
        <br />
        <div class="form-group">
          <button class="btn btn-primary">Update</button>
        </div>
    </form>
  </div>
</template>

<script>
    export default {

      data() {
        return {
          user: {}
        }
      },
      created() {
        let uri = `http://localhost:8000/api/user/edit/${this.$route.params.id}`;
        this.axios.get(uri).then((response) => {
            // console.log(response.data);
            this.user = response.data;
        });
      },
      methods: {
        updateUser() {
          let uri = `http://localhost:8000/api/user/update/${this.$route.params.id}`;
          this.axios.post(uri, this.user).then((response) => {
            this.$router.push({name: 'users'});
          });
        }
      }
    }
</script>