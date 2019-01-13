<template lang="html">
  <section class="section">
    <div class="container">
        <div class="columns">
            <div class="column filter-container">
                <div class="column filter-container" v-for="(filter, index) in filters" :key="index">
                  <b-tooltip :label="filter.popupText" multilined position="is-right" animated>
                    <h3 class="title is-3">{{ filter.title }} Filters:</h3>
                  </b-tooltip>
                  <div v-if="filter.type === 'max-slider' || filter.type === 'min-slider'"><br/>
                    <vue-slider ref="price" v-model="filter.value" :max="filter.data.maxValue" :min="filter.data.minValue"></vue-slider>
                    <div class="choosen-filters">
                      <p>Choosen Value: {{ filter.value }}</p>
                    </div>
                  </div>
                  <div v-if="filter.type === 'checkbox'">
                    <div class="columns is-mobile">
                      <div class="column">
                        <div v-for="filterOption in filter.data">
                          <input class="is-checkradio" type="checkbox" v-model="filter.value" :value="filterOption" />
                            <label>{{ filterOption }}</label>
                        </div>
                      </div>
                    </div>
                  </div>
              </div>
            </div>
          </div>
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
        <div class="buttons are-large is-centered">
          <button class="button is-primary is-focused" @click="applyFilters">Apply</button>
          <button class="button is-warning is-focused" @click="clear">Clear</button>
        </div>
    </div>
</section>
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
          type: 'max-slider',
          title: 'MaxPrice',
          name: 'price',
          value: 32000,
          data: {
            minValue: 0,
            maxValue: 32000
          },
          popupText: 'Here you can see the range filters!'
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
    checkedFilters () {
      return this.filters.map(filter => filter.value)
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
  margin: 20px;
}
.choosen-filters {
  margin: 20px 0px 20px 0px;
}
</style>


