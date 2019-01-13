<template lang="html">
  <div>
    <h4 class="title is-4">Checked Filters:</h4>
    <span v-if="checkedFilters.length">{{ checkedFilters }}</span>
    <span class="has-text-danger" v-else>No Filters Choosen!</span>
  </div>
</template>
<script>
export default {
  name: 'checked-filters',
  props: {
    checkedFilters: Array
  },
  data () {
    return {}
  }
}
</script>

