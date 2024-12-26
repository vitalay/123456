<template>
  <input v-model="newPoint">
<button @click="save" >save</button>

</template>

<script>
export default {
  emits: ['add'],
  data() {
    return{
      newPoint: '',
    }
  },
  methods: {
    save(){
      this.$emit('add', this.newPoint);
      this.newPoint = '';
    }
      
  }
}

</script>



<style>
</style>