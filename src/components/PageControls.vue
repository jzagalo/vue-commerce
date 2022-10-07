<template>
  <div class="row mt-2">
    <div class="col form-group">
      <select class="form-control" @change="changePageSize">
        <option value="4">4 per Page</option>
        <option value="8">8 per Page</option>
        <option value="12">12 per Page</option>
      </select>
    </div>
    <div v-if="pageCount > 1" class="text-right col">
      <div class="bt-group mx-2">
        <button v-for="i in pageNumbers"
                :key="i" class="btn"
                @click="setCurrentPage(i)"
                :class="{ 'btn-primary' : i == currentPage }">
          {{i}}
        </button>
      </div>
    </div>
  </div>
</template>

<script>

import { mapState, mapGetters, mapMutations } from "vuex";

export default {

  methods:{
     ...mapMutations(["setCurrentPage", "setPageSize"]),
    changePageSize($event){
       this.setPageSize(Number($event.target.value))
    }
  },
  computed:{
    ...mapState(["currentPage"]),
    ...mapGetters(["pageCount"]),
    pageNumbers(){
      return [...Array(this.pageCount+1).keys()].slice(1)
    }
  }
}
</script>

<style scoped>

</style>