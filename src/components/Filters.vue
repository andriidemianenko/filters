<template lang="html">
  <section>
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
  </section>
</template>
<script>
import vueSlider from 'vue-slider-component'

export default {
  name: 'filters',
  components: { vueSlider },
  props: {
    gooods:  Array,
    filters: Array
  },
  data () {
    return {}
  }
}
</script>
