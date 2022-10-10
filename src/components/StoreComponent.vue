<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col bg-dark text-white">
        <a href="#" class="navbar-brand">SPORT STORE</a>
        <CartSummary />
      </div>
    </div>
    <div class="row">
      <div class="col-3 bg-info p-2">
        <h4 class="text-white m-2">Categories</h4>
        <CategoryControls />
      </div>
      <div class="col-9 bg-success p-2">
        <ProductList />
      </div>
    </div>
  </div>
</template>
<script>
import ProductList from "@/components/ProductList";
import CategoryControls from "@/components/CategoryControls";
import CartSummary from "@/components/CartSummary";

export default {
  components:{
    ProductList,
    CategoryControls,
    CartSummary,
  }

}
</script>

<style scoped>

a.navbar-brand {
  color: white;
  text-align:left;
}

</style>