<template>
  <div class="income-item">
    <div class="remove-item" @click="removeItem">x</div>
    <div class="desc">{{ income.desc }}</div>
    <div class="price">€{{ income.value }}</div>
    <div class="date">{{ formattedDate }}</div>
  </div>
</template>

<script>
export default {
  props: {
    income: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      formattedDate: this.formatDate(this.income.date)
    };
  },
  methods: {
    formatDate(timestamp) {
      const date = new Date(timestamp);
      const day = date.getDate();
      const month = date.getMonth() + 1;
      const year = date.getFullYear();
      return `${day}/${month}/${year}`;
    },
    removeItem() {
      this.$emit('remove-item', this.income.id);
    }
  }
};
</script>

<style scoped>
.income-item {
  position: relative;
  display: flex;
  padding: 15px 15px 15px 0px;
  background-color: #fff;
  border-radius: 8px;
  max-width: 600px;
  margin: 0 auto 30px;
}

.remove-item {
  color: #ef2d2d;
  font-weight: 600;
  font-size: 20px;
  line-height: 1;
  text-align: center;
  margin: 0 15px;
  cursor: pointer; /* Ensure the cursor indicates it's clickable */
}

.desc {
  color: #666;
  flex: 1 1 100%;
  font-size: 20px;
}

.price {
  color: #666;
  min-width: 100px;
  font-size: 20px;
}

.date {
  color: #666;
  text-align: right;
  font-size: 20px;
}
@media (max-width: 768px) {
  .income-item {
    max-width: 90vw; /* Přizpůsobení maximální šířky na menších obrazovkách */
  }
}

@media (max-width: 480px) {
  .income-item {
    max-width: 100%; /* Plná šířka pro mobilní obrazovky */
  }
}
</style>
