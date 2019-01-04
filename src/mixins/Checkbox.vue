<script>
export default {
  name: 'checkbox-filters',
  props: {
    goods: Array
  },
  data () {
    return {
      checkedFilters: [],
      colorFilters: ['red', 'black', 'white', 'blue', 'green'],
      brandFilters: ['Meizu', 'Xiaomi', 'Apple', 'Dell', 'HP']
    }
  },
  computed: {},
  methods: {},
  created () {}
}
</script>

