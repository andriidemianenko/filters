<template lang="pug">
  section
    h1 {{ test }}
</template>

<script>
export default {
  name: 'slider-filters',
  props: {
    data: Array
  },
  data () {
    return {
      test: 'Sliders!'
    }
  },
  computed: {},
  methods: {},
  created () {
    console.log(this.data)
  }
}
</script>

