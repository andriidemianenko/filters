<template lang="html">
  <div class="columns filter-container">
    <div class="column">
      <h4 class="title is-4">Checked Filters:</h4>
      <span v-if="checkedFilters.length">{{ checkedFilters }}</span>
      <span class="has-text-danger" v-else>No Filters Choosen!</span>
    </div>
    <div class="column filter-container">
      <h4 class="title is-4">Matching Goods:</h4>
      <span v-if="filteredGoods.length">{{ filteredGoods }}</span>
      <span class="has-text-danger" v-else>There are no goods matching this filters!</span>
    </div>
  </div>
</template>
<script>
export default {
  name: 'display',
  props: {
    checkedFilters: Array,
    filteredGoods: Array
  },
  data () {
    return {}
  }
}
</script>

