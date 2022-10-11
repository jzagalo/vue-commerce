<template>
  <div>
    <div class="container-fluid">
      <div class="row">
        <div class="col bg-dark text-white">
          <a class="navbar-brand">SPORTS STORE</a>
        </div>
      </div>
    </div>
    <div class="m-2">
      <div class="form-group m-2">
        <label for="name">Name</label>
        <input v-model="$v.order.name.$model" class="form-control" />
        <validation-error :validation="$v.order.name" />
      </div>
    </div>
    <div class="m-2">
      <div class="form-group m-2">
        <label for="name">Email</label>
        <input v-model="$v.order.email.$model" class="form-control" />
        <validation-error :validation="$v.order.email" />
      </div>
    </div>
    <div class="m-2">
      <div class="form-group m-2">
        <label for="name">City</label>
        <input v-model="$v.order.city.$model" class="form-control" />
        <validation-error :validation="$v.order.city" />
      </div>
    </div>
    <div class="m-2">
      <div class="form-group m-2">
        <label for="name">Zip</label>
        <input v-model="$v.order.zip.$model" class="form-control" />
        <validation-error :validation="$v.order.zip" />
      </div>
    </div>
    <div class="text-center">
      <router-link to="/cart" class="btn btn-secondary m-1">
        Back
      </router-link>
      <button class="btn btn-primary m-1" @click="submitOrder">
        Place Order
      </button>
    </div>
  </div>

</template>

<script>
import ValidationError from "@/ValidationError";
import { required, email } from "vuelidate/lib/validators";
import {mapActions} from "vuex";

export default {
  name: "CheckOut",
  components: {ValidationError},
  data(){
    return {
      order: {
        name: null,
        email: null,
        address: null,
        city: null,
        zip: null
      }
    }
  },
  validations: {
    order: {
      name: { required },
      email: { required, email },
      address: { required },
      city: { required },
      zip: { required }
    }
  },
  methods: {
    ...mapActions({
      "storeOrder": "storeOrder",
      "clearCart": "cart/clearCartData"
    }),
    async submitOrder(){
      this.$v.$touch();
      if( this.$v.$invalid){
        let order = await this.storeOrder(this.order)
        this.clearCart();
        this.$router.push(`/thanks/${order}`)
      }
    }
  }
}
</script>

<style scoped>

</style>