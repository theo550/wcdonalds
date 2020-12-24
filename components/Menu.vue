<template>
  <div @click="addThisItem" class="card-menu">
    <img :src="url" :alt="name">
    <h6>{{ name }}</h6>
  </div>
</template>

<script>
export default {
  props: ['name', 'item', 'url'],
  methods: {
    addThisItem() {
      return this.$emit('add', this.item)
    }
  }
}
</script>

<style scoped>

 .card-menu{
   height: 100px;
   width: 100px;
   background-color: #F8F8F8;
   display: flex;
   flex-direction: column;
   align-items: center;
   justify-content: center;
   border-radius: 30px;
   margin: 10px;
   cursor: pointer;
 }

 .card-menu:hover{
   background-color: #f4f4f4;
 }

 h6{
   margin-top: 10px;
 }

 .card-menu img {
   height: 50px;
 }

</style>