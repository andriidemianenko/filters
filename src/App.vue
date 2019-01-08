<template lang="pug">
  section.section
    .container
      .columns
        .column.filter-container
          .column.filter-container(v-for="(filter, index) in filters", :key="index")
            h3.title.is-3 {{ filter.title }} Filters:
            div(v-if="filter.type === 'range'")
              vue-slider(ref="price", v-model="filter.value", :max="filter.data.maxValue", :min="filter.data.minValue")
              .choosen-filters
                p Choosen Value: {{ filter.value }}
            div(v-if="filter.type === 'checkbox'")
              .columns.is-mobile
                .column
                  ul
                    li(v-for="filterOption in filter.data")
                      input.is-checkradio(type="checkbox", v-model="filter.value", :value="filterOption") 
                      label {{ filterOption }}
      .columns.filter-container
        .column
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
import vueSlider from 'vue-slider-component'

export default {
  components: { vueSlider },
  data () {
    return {
      filteredGoods: [],
      filters: [
        {
          type: 'checkbox',
          title: 'Brand',
          value: [],
          data: ['Meizu', 'Xiaomi', 'Apple', 'Dell', 'HP']
        },
        {
          type: 'checkbox',
          title: 'Colors',
          value: [],
          data: ['red', 'black', 'white', 'blue', 'green']
        },
        {
          type: 'range',
          title: 'MaxPrice',
          value: 20000,
          data: {
            minValue: 0,
            maxValue: 32000
          }
        }
      ],
      // price: 20000,
      // minValue: 0,
      // maxValue: 32000,
      // colorFilters: ['red', 'black', 'white', 'blue', 'green'],
      // brandFilters: ['Meizu', 'Xiaomi', 'Apple', 'Dell', 'HP'],
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
          price: 30000,
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
  computed: {
    checkedFilters () {
      return this.filters.map(filter => filter.value)
    }
  },
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


