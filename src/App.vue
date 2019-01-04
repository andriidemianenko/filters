<template lang="pug">
  section
    section
      h1 Sliders Filters:
      vue-slider(ref="price", v-model="price", :max="maxValue", :min="minValue")
      span {{ price }}
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
    br
    span(v-show="filteredGoods.length > 0") {{ filteredGoods }}
    button(@click="applyFilters") Apply
    button(@click="clear") Clear
</template>

<script>
import SliderFilters from './mixins/Sliders.vue'
import CheckboxFilters from './mixins/Checkbox.vue'

export default {
  mixins: [ SliderFilters, CheckboxFilters ],
  data () {
    return {
      filteredGoods: [],
      defaultGoods: [
        {
          price: 7400,
          color: 'black',
          type: 'laptops',
          producer: 'Dell'
        },
        {
          price: 4500,
          color: 'red',
          type: 'smart-phone',
          producer: 'Xiaomi'
        },
        {
          price: 70000,
          color: 'white',
          type: 'laptops',
          producer: 'Apple'
        },
        {
          price: 8000,
          color: 'white',
          type: 'smart-phone',
          producer: 'Meizu'
        },
        {
          price: 20300,
          color: 'blue',
          type: 'laptops',
          producer: 'Dell'
        },
        {
          price: 9000,
          color: 'red',
          type: 'smart-phone',
          producer: 'Meizu'
        },
        {
          price: 800,
          color: 'green',
          type: 'accessories',
          producer: 'Xiaomi'
        },
        {
          price: 25000,
          color: 'black',
          type: 'laptops',
          producer: 'HP'
        }
      ]
    }
  }, 
  computed: {},
  methods: {
    applyFilters () {
     console.log('Clicked Apply!')
    },
    clear () {
      this.filteredGoods = []
    }
  },
  created () {}
}
</script>
<style>
.checked-filters {
  float: left;
  color: green;
}
</style>


