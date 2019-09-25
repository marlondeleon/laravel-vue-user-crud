<template>
    <div>
        <div class="form-group text-right">
            <router-link :to="{name: 'createUser'}" class="btn btn-success">Create new company</router-link>
        </div>
        <div class="panel panel-default">
            <div class="panel-heading">Users list</div>
            <div class="panel-body">
                <table class="table table-bordered table-striped">
                    <thead>
                        <tr>
                            <th class="text-center">Name</th>
                            <th class="text-center">Email</th>
                            <th class="text-center">Created At</th>
                            <th class="text-center" width="200">Action</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="user in users.data" :key="user.id">
                            <td>{{ user.name }}</td>
                            <td>{{ user.email }}</td>
                            <td>{{ user.created_at }}</td>
                            <td class="text-center">
                                <router-link :to="{name: 'editUser', params: {id: user.id}}" class="btn btn-sm btn-outline-secondary">
                                    <i class="fa fa-edit"></i> 
                                </router-link>
                                <!-- <a href="#" class="btn btn-sm btn-outline-danger" v-on:click="deleteUser(user.id)">
                                    <i class="fas fa-trash-alt"></i>
                                </a> -->
                                <button class="btn btn-sm btn-outline-danger" @click="deleteUser(user.id)"><i class="fas fa-trash-alt"></i></button>
                            </td>
                        </tr>
                    </tbody>
                </table>
                <pagination :data="users" @pagination-change-page="getResults"></pagination>
                
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                users: {},
                limit: 2,
                showDisabled: false,
                size: 'small',
                align: 'left'
            }
        },
        // created() {
        //     let uri = 'http://localhost:8000/api/users';
        //     this.axios.get(uri).then(response => {
        //         this.users = response.data.data;
        //     });
        // },
        mounted() {
            // Fetch initial results
            this.getResults();
        },
        methods: {
            deleteUser(id)
            {
                console.log(id);
                let uri = `http://localhost:8000/api/user/delete/${id}`;
                // this.axios.delete(uri).then(response => {
                //     // this.users.splice(this.users.indexOf(id), 1);
                //     // this.$router.push({name: 'users'});
                //         // this.users.splice(this.users.indexOf(id), 1).push(response.data);


                //     const index = this.users.findIndex(user => user.id === id) // find the post index 
                //         if (~index) // if the post exists in array
                //             this.users.splice(index, 1) //delete the post
                // });

                this.axios.delete(uri).then(response => {
                    return this.getResults();
                })
               
            },
            getResults(page) {
                if (typeof page === 'undefined') {
                    page = 1;
                }
                axios.get('http://localhost:8000/api/users?page=' + page)
                    .then(response => {
                        // console.log(response.data.data);
                        this.users = response.data;
                    });
            }
        },
    }
</script>

<style>
    .panel-heading {
        font-weight:700;
        font-size: 1.2em;
    }
</style>