<template lang="pug">
  section.section
    .container
      .columns
        .column.filter-container
          h3.title.is-3 Sliders Filters:
          vue-slider(ref="price", v-model="price", :max="maxValue", :min="minValue")
          .choosen-filters
            p Choosen Value: {{ price }}
          .columns.is-mobile
            .column.filter-container
              h3.title.is-3 Color Checkbox Filters:
              ul
                li(v-for="(color, index) in colorFilters")
                  input.is-checkradio(type="checkbox", v-model="checkedFilters", :value="color") 
                  label {{ color }}
            .column.filter-container
              h3.title.is-3 Brand Checkbox Filters:
              ul
                li(v-for="(brand, index) in brandFilters")
                  input(type="checkbox", v-model="checkedFilters", :value="brand")
                  label {{ brand }}
      .columns
        .column.filter-container
          h4.title.is-4 Checked Filters:
          span(v-if="checkedFilters.length") {{ checkedFilters }}
          span.has-text-danger(v-else) No Filters Choosen!
        .column.filter-container
          h4.title.is-4 Matching Goods:
          span(v-if="filteredGoods.length") {{ filteredGoods }}
          span.has-text-danger(v-else) There are no goods matching this filters!
      .buttons.are-large.is-centered
        button.button.is-primary.is-focused(@click="applyFilters") Apply
        button.button.is-warning.is-focused(@click="clear") Clear
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
     this.filteredGoods = this.defaultGoods.filter(el => {
        return (el.price <= this.price) && this.checkedFilters.every(filterAppied => {
          if (el.color.includes(filterAppied)) {
            return el.color.includes(filterAppied)
          }
          if (el.producer.includes(filterAppied)) {
            return el.producer.includes(filterAppied)
          }
        })
      })
    },
    clear () {
      this.filteredGoods = []
      this.checkedFilters = []
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
.filter-container {
  border: 2px #4978cf solid;
  margin: 20px;
}
.choosen-filters {
  margin: 20px 0px 20px 0px;
}
</style>


