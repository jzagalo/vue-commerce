<template>
  <div>
    <div v-for="p in products" :key="p.id" class="card m-1 p-1 bg-light">
      <div class="d-flex justify-content-between align-items-start">
        <h4>
          <p class="text-left">{{ p.name }}</p>
          <div class="card-text bg-white p-1">
            {{ p.description }}
          </div>
        </h4>
        <div>
          <h4>
            <span class="badge badge-pill badge-primary float-right">
            {{ p.price | currency }}
          </span>
          </h4>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
import { mapState } from "vuex"

export default {
  name: "ProductList.vue",
  computed:{
    ...mapState([ "products" ])
  },
  filters: {
    currency(value){
      return new Intl.NumberFormat("en-US", { style: "currency", currency: "USD"}).format(value)
    }
  }
}
</script>

<style scoped>

</style>