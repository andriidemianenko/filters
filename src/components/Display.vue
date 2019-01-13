<template lang="html">
  <div class="columns">
    <div class="column filter-container">
      <h4 class="title is-4">Matching Goods:</h4>
      <div v-if="filteredGoods.length">
        <b-message type="is-info" v-for="(product, index) in filteredGoods" :key="product.price + index">
          <span><b>Producer:</b> {{ product.producer }}</span></br>
          <span><b>Product Type:</b> {{ product.type }}</span></br>
          <span><b>Color:</b> {{ product.color }}</span></br>
          <span><b>Price:</b> {{ product.price }}</span>
        </b-message>
      </div>
      <span class="has-text-danger" v-else>There are no goods matching this filters!</span>
    </div>
  </div>
</template>
<script>
export default {
  name: 'display',
  props: {
    filteredGoods: Array
  },
  data () {
    return {}
  }
}
</script>

