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
      <button :disabled="currentPage === 1"
              @click="setCurrentPage(currentPage - 1)"
              class="btn mx-1">Previous</button>
      <span v-if="currentPage > 4">
        <button class="btn mx-1"
                @click="setCurrentPage(1)">1
        </button>
        <span class="h4">...</span>
      </span>
      <span v-if="currentPage <= pageCount-4">
        <span class="h4">...</span>
        <button class="btn mr-2"
                @click="setCurrentPage(pageCount)">{{ pageCount }} </button>
      </span>
      <span v-if="currentPage > 4">
        <button class="btn"
                v-for="i in pageNumbers"
                :key="i"
                :class="{ 'btn-primary' : i === currentPage }"
                @click="setCurrentPage(i)">{{ i }}</button>
      </span>
      <button class="btn ml-1"
              :disabled="currentPage === pageCount"
              @click="setCurrentPage(currentPage + 1)">Next</button>
    </div>
  </div>
</template>

<script>

import {mapState, mapGetters, mapActions} from "vuex";

export default {

  methods:{
     ...mapActions(["setCurrentPage", "setPageSize"]),
    changePageSize($event){
       this.setPageSize($event.target.value)
    }
  },
  computed:{
    ...mapState(["currentPage"]),
    ...mapGetters(["pageCount"]),
    pageNumbers(){
      if(this.pageCount < 4) {
        return [...Array(this.pageCount + 1).keys()].slice(1)
      }else if(this.currentPage <= 4) {
        return [1, 2, 3, 4, 5]
      }else if(this.currentPage > this.pageCount - 4){
        return [ ...Array(5).keys()].reverse().map(v => this.pageCount - v)
      }else{
        return [ this.currentPage - 1, this.currentPage, this.currentPage + 1 ]
      }
    }
  }
}
</script>

<style scoped>

</style>