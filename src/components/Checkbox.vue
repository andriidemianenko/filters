<template lang="pug">
  section
    h1 {{ test }}
</template>

<script>
export default {
  name: 'checkbox-filters',
  props: {
    data: Array
  },
  data () {
    return {
      test: 'Checkboxes!'
    }
  },
  computed: {},
  methods: {},
  created () {
    console.log(this.data)
  }
}
</script>
