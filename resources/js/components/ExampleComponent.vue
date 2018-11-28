<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-12">
                <div class="card card-default">
                    <div class="card-header">Customer Table</div>

                    <div class="card-body">
                        <table class="table table-bordered">
                              <thead>
                                <tr>
                                  <th scope="col">Id</th>
                                  <th scope="col">Name</th>
                                  <th scope="col">Email</th>
                                  <th scope="col">Phone</th>
                                  <th scope="col">Address</th>
                                  <th scope="col">Total</th>
                                </tr>
                              </thead>
                              <tbody>
                                <tr v-for="cust in custs.data">
                                  <th scope="row">{{cust.id}}</th>
                                  <td>{{cust.name}}</td>
                                  <td>{{cust.email}}</td>
                                  <td>{{cust.phone}}</td>
                                  <td>{{cust.address}}</td>
                                  <td>{{cust.total}}</td>
                                </tr>
                              </tbody>
                        </table>
                              
                                <div class="d-flex justify-content-center">
                                     <pagination :data="custs"@pagination-change-page="getResults" :limit="4">
                                            <span slot="prev-nav">&lt; Previous</span>
                                            <span slot="next-nav">Next &gt;</span>
                                     </pagination>
                                </div>

                               
                             
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
Vue.component('pagination', require('laravel-vue-pagination'));

    export default {

        data(){
            return{
                custs:{},
            }
        },
        methods:{

            getResults(page = 1) {
            axios.get('http://127.0.0.1:8000/api/customer/?page=' + page)
                .then((response) => this.custs = response.data)
                .catch((error) => console.log(error));
                 console.log('Component mounted.');
            }


        },

        created() {
            axios.get('http://127.0.0.1:8000/api/customer')
            .then((response) => this.custs = response.data)
            .catch((error) => console.log(error));
            console.log('Component mounted.');
        }
        
        
    }
</script>
<style type="text/css" scoped>
    
</style>