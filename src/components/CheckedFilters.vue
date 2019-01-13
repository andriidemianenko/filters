<template lang="html">
  <section>
    <h4 class="title is-4">Checked Filters:</h4>
    <div class="columns">
      <div class="column">
        <h6 class="title is-6">Checkbox Filters:</h6>
        <div v-if="checkboxFilters.length">
          <div class="content">
            <ul>
              <li v-for="filterVal in checkboxFilters"><span>{{ filterVal }}</span></li>
            </ul>
          </div>
        </div>
        <span class="has-text-danger" v-else>No Checkbox filters Choosen!</span>
      </div>
      <div class="column">
        <h6 class="title is-6">Silder Filters:</h6>
        <div v-if="sliderFilters.length">
          <span>{{ sliderFilters }}</span>
        </div>
        <span class="has-text-danger" v-else>No Slider filters Choosen!</span>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  name: 'checked-filters',
  props: {
    checkboxFilters: Array,
    sliderFilters: Array
  },
  data () {
    return {}
  }
}
</script>

