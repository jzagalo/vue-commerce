<template>
  <tr>
    <td>
      <input type="number" class="form-control-sm" style="width: 5em" :min="0" :value="qvalue" @input="sendChangeEvent" />
    </td>
    <td>{{ line.product.name }}</td>
    <td class="text-right">{{ line.product.price | currency }}</td>
    <td class="text-right">{{ (line.product.price * line.quantity ) | currency }}</td>
    <td class="text-right">
      <button class="btn btn-sm btn-danger" @click="sendRemoveEvent">Remove</button>
    </td>
  </tr>
</template>

<script>
export default {
  name: "ShoppingCartLine",
  props: {
    line: Object,
  },
  data(){
    return {
      qvalue: this.line.quantity
    }
  },
  methods: {
    sendChangeEvent($event){
      if($event.target.value){
        this.$emit("quantity", Number($event.target.value))
        this.qvalue = $event.target.value;
      }else {
        this.$emit("quantity", 1);
        this.qvalue = 1;
        $event.target.value = this.qvalue;
      }
    },
    sendRemoveEvent(){
      this.$emit("remove", this.line)
    },
  }
}
</script>

<style scoped>

</style>