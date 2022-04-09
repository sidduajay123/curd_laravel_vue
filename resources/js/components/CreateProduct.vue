<template>
    <div >
        <div>
            <h3 class="text-center">Create</h3>
            <div class="row">
                <div class="col-md-6">
                    <form @submit.prevent="addProduct">
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
                        <button type="submit" class="btn btn-primary">Create</button>
                    </form>
                </div>
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
        methods: {
            addProduct() {
                this.axios
                    .post('http://localhost:8080/api/products', this.product)
                    .then(response => (
                        this.$router.push({ name: 'home' })
                    ))
                    .catch(err => console.log(err))
                    .finally(() => this.loading = false)
            },
            show() {
                this.showModal = true
            },
            hide(){
                this.showModal = false
            }
        }
    }
</script>