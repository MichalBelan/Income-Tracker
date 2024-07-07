<!-- eslint-disable vue/no-side-effects-in-computed-properties -->
<template>
  <div>
    <Header :totalIncome="totalIncome" />
    <Form @add-income="AddIncome" />
    <IncomeList :state="state" @remove-item="removeItem" />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Form from './components/Form.vue'
import IncomeList from './components/IncomeList.vue'

export default {
  data() {
    return {
      state: {
        income: []
      }
    }
  },
  components: {
    // eslint-disable-next-line vue/no-reserved-component-names
    Header,
    // eslint-disable-next-line vue/no-reserved-component-names
    Form,
    IncomeList
  },
  computed: {
    sortedIncome() {
      return [...this.state.income].sort((a, b) => b.date - a.date);
    },
    totalIncome() {
      return this.state.income.reduce((total, item) => total + item.value, 0);
    }
  },
  methods: {
    AddIncome(obj) {
      let d = obj.date.split('-');
      let newD = new Date(d[0], d[1] - 1, d[2]); // Month is zero-indexed in Date constructor

      this.state.income.push({
        id: Date.now(),
        desc: obj.desc,
        value: parseInt(obj.value),
        date: newD.getTime()
      });
    },
    removeItem(id) {
      this.state.income = this.state.income.filter((v) => v.id != id);
    }
  }
}
</script>

<style scoped>

</style>
