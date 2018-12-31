<template lang="pug">
  section
    h1 Sliders Filters:
    vue-slider(ref="price", v-model="price", :max="maxValue", :min="minValue")
    span {{ price }}
</template>

<script>
import vueSlider from 'vue-slider-component';

export default {
  name: 'slider-filters',
  props: {
    goods: Array
  },
  components: { vueSlider },
  data () {
    return {
      price: 35000,
      minValue: 0,
      maxValue: 80000
    }
  },
  computed: {},
  methods: {},
  created () {
    console.log(this.goods)
  }
}
</script>

