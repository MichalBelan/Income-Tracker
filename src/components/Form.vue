// eslint-disable-next-line vue/multi-word-component-names
<template>
  <form @submit.prevent="FormHandler">
    <input type="text" placeholder="Description..." v-model="formData.desc" />
    <input type="number" placeholder="Value..." v-model.number="formData.value" />
    <input type="date" placeholder="Date..." v-model="formData.date" />
    <input type="submit" value="SUBMIT" />
  </form>
</template>

<script>
export default {
  props: {
    state: Object
  },
  data() {
    return {
      formData: {
        desc: null,
        value: null,
        date: null
      }
    }
  },
  methods: {
    FormHandler() {
      // Emit an 'add-income' event with formData
      this.$emit('add-income', {
        desc: this.formData.desc,
        value: parseFloat(this.formData.value), // Ensure value is parsed as float
        date: this.formData.date
      })

      // Reset formData fields after emitting event
      this.formData.desc = null
      this.formData.value = null
      this.formData.date = null
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}

form input {
  color: #888;
  border: none;
  outline: none;
  font-size: 20px;
}

form input::placeholder {
  color: #aaa;
}

form input:not([type='submit']) {
  display: block;
  background: #fff;
  border: none;
  outline: none;
  padding: 5px 15px;
}

form input[type='submit'] {
  display: block;
  background: none;
  border: none;
  outline: none;
  color: #fff;
  font-weight: 500;
  text-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
  padding: 5px 15px;
  background-color: #ffce00;
  cursor: pointer;
}

form input:first-of-type {
  border-radius: 8px 0px 0px 8px;
}

form input:last-of-type {
  border-radius: 0px 8px 8px 0px;
}

@media (max-width: 768px) {
  .form {
    flex-direction: column; /* Formulářové prvky se zalamují do sloupce */
    align-items: center;
    
  }
}
</style>
