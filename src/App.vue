<template lang="pug">
  section
    slider-filters
    checkbox-filters
</template>


<script>
import SliderFilters from './components/Sliders.vue'
import CheckboxFilters from './components/Checkbox.vue'

export default {
  components: { SliderFilters, CheckboxFilters },
  data () {
    return {
      test: 'Hello World!'
    }
  }
}
</script>

