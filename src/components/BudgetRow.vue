<template>
  <!-- EDIT CODE BELOW -->
  <v-row>
    <v-col cols="2" class="remove">
      <v-btn icon small dark color="primary" @click="remove">
        <v-icon>
          mdi-minus-circle
        </v-icon>
      </v-btn>
    </v-col>
    <v-col cols="5">
      <v-select
        v-model="budgetType"
        label="Budget Type"
        :items="budgetTypes"
        :item-text="(item) => item.name"
        return-object
      />
    </v-col>
    <v-col cols="5">
      <v-text-field
        v-model="amount"
        class="currency-input"
        label="Enter amount"
        type="number"
        prefix="$"
      />
    </v-col>
  </v-row>
</template>

<script>
import { loadBudgetTypes } from "@/mock.js";

export default {
  name: "BudgetRow",
  data() {
    return {
      budgetType: null,
      budgetTypes: [],
      amount: 0,
    };
  },
  props: {
    data: {
      type: Object,
      required: true,
    },
  },
  created() {
    this.budgetTypes = loadBudgetTypes();
  },
  methods: {
    remove() {
      this.$emit("remove", this.data);
    },
  },
  watch: {
    amount() {
      this.$emit("changeTotal", this.data, this.amount);
    },
  },
};
</script>

<style scoped>
.remove {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
