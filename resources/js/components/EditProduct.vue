<template>
    <div>
        <h3 class="text-center">Edit</h3>
        <div class="row">
            <div class="col-md-6">
                <form @submit.prevent="updateProduct">
                    <div class="form-group">
                            <label>Email</label>
                            <input type="email" class="form-control" v-model="product.email">
                        </div>
                        <div class="form-group">
                            <label>User</label>
                            <input type="text" class="form-control" v-model="product.user">
                        </div>
                        <div class="form-group">
                            <label>Author</label>
                            <input type="text" class="form-control" v-model="product.author">
                        </div>
                        <div class="form-group">
                            <label>Country</label>
                            <input type="text" class="form-control" v-model="product.country">
                        </div>
                        <div class="form-group">
                            <label>Status</label>
                            <select class="form-control" v-model="product.status">
                                <option>Select Status</option>
                                <option value="0">InActive</option>
                                <option value="1">Active</option>
                            </select>
                        </div>
                    <button type="submit" class="btn btn-primary">Update</button>
                </form>
            </div>
        </div>
    </div>
</template>
 
<script>
    export default {
        data() {
            return {
                product: {}
            }
        },
        created() {
            this.axios
                .get(`http://localhost:8080/api/products/${this.$route.params.id}`)
                .then((res) => {
                    this.product = res.data;
                });
        },
        methods: {
            updateProduct() {
                this.axios
                    .patch(`http://localhost:8080/api/products/${this.$route.params.id}`, this.product)
                    .then((res) => {
                        this.$router.push({ name: 'home' });
                    });
            }
        }
    }
</script>