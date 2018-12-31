<template lang="pug">
  section
    h1 Checkbox Filters:
    div(id="checkbox-container")
      input(type="checkbox", value="red", v-model="checkedFilters")
      label Red
      input(type="checkbox", value="black", v-model="checkedFilters")
      label Black
      input(type="checkbox", value="white", v-model="checkedFilters")
      label White
      input(type="checkbox", value="blue", v-model="checkedFilters")
      label Blue
      input(type="checkbox", value="green", v-model="checkedFilters")
      label Green
      input(type="checkbox", value="Meizu", v-model="checkedFilters")
      label Meizu
      input(type="checkbox", value="Xiaomi", v-model="checkedFilters")
      label Xiaomi
      input(type="checkbox", value="Apple", v-model="checkedFilters")
      label Apple
      input(type="checkbox", value="Dell", v-model="checkedFilters")
      label Dell
      input(type="checkbox", value="HP", v-model="checkedFilters")
      label HP
      br
      span.checked-filters(v-show="checkedFilters.length > 0") {{ checkedFilters }}
</template>

<script>
export default {
  name: 'checkbox-filters',
  props: {
    goods: Array
  },
  data () {
    return {
      checkedFilters: []
    }
  },
  computed: {},
  methods: {},
  created () {
    console.log(this.goods)
  }
}
</script>
<style>
  .checked-filters {
    float: left;
    color: green;
  }
</style>

