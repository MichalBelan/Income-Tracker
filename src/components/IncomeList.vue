<template>
  <div class="income-list">
    <IncomeItem
      v-for="income in sortedIncome"
      :key="income.id"
      :income="income"
      @remove-item="removeItem"
    />
  </div>
</template>

<script>
import IncomeItem from './IncomeItem.vue'

export default {
  props: {
    state: {
      type: Object,
      required: true
    }
  },
  components: {
    IncomeItem
  },
  computed: {
    sortedIncome() {
      // Sorts the income array in state by date descending
      return [...this.state.income].sort((a, b) => b.date - a.date)
    }
  },
  methods: {
    removeItem(id) {
      // Emits the 'remove-item' event with the income id to be removed
      this.$emit('remove-item', id)
    }
  }
}
</script>

<style scoped>
.income-list {
  margin-top: 30px;
  padding: 15px;
}
@media (max-width: 768px) {
  .income-list {
    flex-direction: column; /* Položky se seznamem se zalamují do sloupce na menších obrazovkách */
    align-items: center;
  }
}
</style>
