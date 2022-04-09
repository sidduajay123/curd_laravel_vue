<template>
    <div>
        <h2 class="text-center">List</h2>
 
        <table class="table table-hover table-bordered" id="example">
            <thead>
            <tr>
                <th>ID</th>
                <th>Email</th>
                <th>User</th>
                <th>Author</th>
                <th>Country</th>
                <th>Status</th>
                <th>Created</th>
                <th>Actions</th> 
            </tr>
            </thead>
            <tbody>
            <tr v-for="product in products" :key="product.id">
                <td>{{ product.id }}</td>
                <td>{{ product.email }}</td>
                <td>{{ product.user }}</td>
                <td>{{ product.author }}</td>
                <td>{{ product.country }}</td>
                <td>{{ (product.status == 1)?'Active':'InActive' }}</td>
                <td>{{ product.created_at }}</td>
                <td>
                    <div class="btn-group" role="group">
                        <router-link :to="{name: 'edit', params: { id: product.id }}" class="btn btn-success">Edit</router-link>
                        <button class="btn btn-danger" @click="deleteProduct(product.id)">Delete</button>
                    </div>
                </td>
            </tr>
            </tbody>
        </table>
    </div>
</template>
<style>
.toolbar {
    float:right;
}
</style>
 
<script>
import $ from 'jquery';
import 'bootstrap/dist/css/bootstrap.min.css';
import 'jquery/dist/jquery.min.js';
import 'datatables.net-dt/js/dataTables.dataTables'
import 'datatables.net-dt/css/jquery.dataTables.min.css';
import modal from './CreateProduct.vue';
    export default {
        components: { modal },
        data() {
            return {
                products: []
            }
        },
        created() {
            this.axios
                .get('http://localhost:8080/api/products/')
                .then(response => {
                    this.products = response.data;
                    setTimeout(() => {
                    $("#example").DataTable({
                        dom: 'l<"toolbar">frtip',
                        // initComplete: function(){
                        //     $("div.toolbar").html('<modal ref="modal"></modal><button @click="openModal">Create</button>');           
                        // } 
                    })
                    }, 250)
                    // $("#example").DataTable();
                });
        },
        methods: {
            deleteProduct(id) { 
                this.axios
                    .delete(`http://localhost:8080/api/products/${id}`)
                    .then(response => {
                        let i = this.products.map(data => data.id).indexOf(id);
                        this.products.splice(i, 1)
                    });
            },
            openModal() { this.$refs.modal.show() }
        }
    }
</script>