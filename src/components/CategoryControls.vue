<template>
  <div class="container-fluid">
    <div class="row my-2" v-for="c in categories" :key="c">
      <button @click="setCurrentCategory(c)"
              class="btn btn-block"
              :class="{ 'btn-primary': c === currentCategory }">
        {{ c }}
      </button>
    </div>
  </div>

</template>

<script>
import { mapGetters, mapState, mapActions} from "vuex";

export default {
  methods: {
    ...mapActions(['setCurrentCategory'])
  },
  computed: {
    ...mapState(['currentCategory']),
    ...mapGetters(['categories'])
  }
}
</script>

<style scoped>

</style>