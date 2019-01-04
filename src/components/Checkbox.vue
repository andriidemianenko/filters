<template lang="pug">
  section
    div
      h1 Color Checkbox Filters:
      ul
        li(v-for="(color, index) in colorFilters")
          input(type="checkbox", v-model="checkedFilters", :value="color") 
          label {{ color }}
    div
      h1 Brand Checkbox Filters:
      ul
        li(v-for="(brand, index) in brandFilters")
          input(type="checkbox", v-model="checkedFilters", :value="brand") 
          label {{ brand }}
    br
    span.checked-filters(v-show="checkedFilters.length > 0") {{ checkedFilters }}
</template>

<script>
export default {
  name: 'checkbox-filters',
  props: {
    goods: Array
  },
  data () {
    return {
      checkedFilters: [],
      colorFilters: ['red', 'black', 'white', 'blue', 'green'],
      brandFilters: ['Meizu', 'Xiaomi', 'Apple', 'Dell', 'HP']
    }
  },
  computed: {},
  methods: {},
  created () {
    console.log(this.goods)
  }
}
</script>
<style>
  .checked-filters {
    float: left;
    color: green;
  }
</style>

