<template lang="pug">
  section
    slider-filters(:data="defaultGoods")
    checkbox-filters(:data="defaultGoods")
</template>

<script>
import SliderFilters from './components/Sliders.vue'
import CheckboxFilters from './components/Checkbox.vue'

export default {
  components: { SliderFilters, CheckboxFilters },
  data () {
    return {
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
  methods: {},
  created () {}
}
</script>

