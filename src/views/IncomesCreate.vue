<template>
  <div class="incomes-create">
    <form v-on:submit.prevent="incomeCreate()">
      <h1>Create Income</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Date:</label>
        <input type="date" v-model="newIncomeParams.date" />
      </div>
      <div>
        <label>Amount:</label>
        <input type="text" v-model="newIncomeParams.amount" />
      </div>
      <div>
        <label>Category:</label>
        <input type="text" v-model="newIncomeParams.category" />
      </div>
      <div>
        <label>Description:</label>
        <input type="text" v-model="newIncomeParams.description" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newIncomeParams: {},
      errors: [],
    };
  },
  created: function () {},
  methods: {
    incomeCreate: function () {
      axios
        .post("/incomes", this.newIncomeParams)
        .then((response) => {
          console.log(response.data);
          this.newIncomeParams = {};
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    clearNewParams: function () {
      this.newIncomeParams = {};
    },
  },
};
</script>
