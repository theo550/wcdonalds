<template>
  <div class="card-lt">
    <img :src="link"  :alt="name">
    <h4>{{ name }}</h4>
    <p>${{ price }}</p>
    <div class="btn-card-lt">
      <button @click="countMinus" class="btn btn-minus">-</button>
      <h4>{{ count }}</h4>
      <button @click="countPlus" class="btn btn-plus">+</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['price', 'count', 'name', 'order', 'link'],
  methods: {
    countMinus (){
      return this.$emit('supTo', this.order)
    },
    countPlus(){
      this.$emit('addTo', this.order)
    }
  }
 }
</script>