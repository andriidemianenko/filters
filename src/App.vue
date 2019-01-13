<template lang="html">
  <section class="section">
    <div class="container">
        <div class="columns filter-container">
          <div class="column filter-container">
            <checked-filters :checkboxFilters="checkboxFilters" :sliderFilters="sliderFilters"></checked-filters>
          </div>
          <div class="column">
            <div class="buttons is-centered">
              <button class="button is-primary is-focused is-fullwidth" @click="applyFilters">Apply</button>
              <button class="button is-warning is-focused is-fullwidth" @click="clear">Clear</button>
            </div>
          </div>
        </div>
        <filters :goods="defaultGoods" :filters="filters"></filters> 
        <display :filteredGoods="filteredGoods"></display>
    </div>
</section>
</template>

<script>
import Filters from './components/Filters.vue'
import Display from './components/Display.vue'
import CheckedFilters from './components/CheckedFilters.vue'

export default {
  components: { Filters, Display, CheckedFilters },
  data () {
    return {
      filteredGoods: [],
      filters: [
        {
          type: 'checkbox',
          title: 'Brand',
          name: 'producer',
          value: [],
          data: ['Meizu', 'Xiaomi', 'Apple', 'Dell', 'HP'],
          popupText: 'Here you can see the Brand filters!'
        },
        {
          type: 'checkbox',
          title: 'Colors',
          name: 'color',
          value: [],
          data: ['red', 'black', 'white', 'blue', 'green'],
          popupText: 'Here you can see the Color filters!'
        },
        {
          type: 'min-slider',
          title: 'MinPrice',
          name: 'price',
          value: 0,
          data: {
            minValue: 0,
            maxValue: 32000
          },
          popupText: 'Here you can see the range filters!'
        },
        {
          type: 'max-slider',
          title: 'MaxPrice',
          name: 'price',
          value: 32000,
          data: {
            minValue: 0,
            maxValue: 32000
          },
          popupText: 'Here you can see the range filters!'
        }
      ],
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
    checkboxFilters () {
      let checkboxFilters = []
      this.filters.forEach(filter => {
        if (filter.type === 'checkbox') {
          filter.value.forEach(filterVal => {
            checkboxFilters.push(filterVal)
          }) 
        }
      })
      return checkboxFilters
    },
    sliderFilters () {
      let sliderFilters = []
      this.filters.forEach(filter => {
        if (filter.type === 'max-slider' || filter.type === 'min-slider') {
          sliderFilters.push(filter.value)
        }
      })
      return sliderFilters
    }
  },
  methods: {
    applyFilters () {
      this.filteredGoods = this.defaultGoods.filter(el => {
        return undefined === this.filters.find(filter => {
          switch(filter.type) {
            case 'checkbox':
              if (!filter.value.length) {
                return false
              } else {
                return !filter.value.includes(el[filter.name])
              }
            case 'max-slider':
              return !(el[filter.name] < filter.value)
            case 'min-slider':
              return !(el[filter.name] > filter.value)
          }
        })
      })
      this.updateFilters()
    },
    clear () {
      this.filters.forEach(filter => {
        if (filter.type === 'checkbox') {
          filter.value = []
        } else if (filter.type === 'max-slider' || filter.type === 'min-slider') {
          filter.value = 0
        }
      })
    },
    updateFilters () {
      this.axios.post('https://some-endpoint.com/', this.filteredGoods)
        .then(res => {
          console.log(res)
        })
        .catch(err => {
          console.log(err)
        })
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
}
.column {
  margin: 20px;
}
.choosen-filters {
  margin: 20px 0px 20px 0px;
}
</style>


