<template>
  <div>
    <div v-for="p in products" :key="p.id" class="card m-1 p-1 bg-light">
      <div class="d-flex justify-content-between align-items-center">
        <h4>
          <p class="text-left">{{ p.name }}</p>
          <div class="card-text bg-white p-1">
            {{ p.description }}
          </div>
        </h4>
        <div class="d-flex flex-column">
          <h4>
            <span class="badge badge-pill badge-primary float-right">
            {{ p.price | currency }}
            </span>
          </h4>
          <div>
            <button class="btn btn-success btn-sm float-right"
                    @click="handleProductAdd(p)">
              Add to Cart
            </button>
          </div>
        </div>
      </div>
    </div>
    <PageControls />
  </div>
</template>

<script>
import {mapGetters, mapState, mapMutations } from "vuex"
import PageControls from "@/components/PageControls";

export default {
  components: {
    PageControls,
  },
  computed:{
    ...mapState([ "products" ]),
    ...mapGetters({ products: "processedProducts" })
  },
  methods: {
    ...mapMutations({ addProduct : "cart/addProduct" }),
    handleProductAdd(product){
      this.addProduct(product);
      this.$router.push("/cart");
    }
  }
}
</script>

<style scoped>

</style>