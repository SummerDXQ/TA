<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12" class="my-4">
        <div class="text-h4 mb-3">Task 4</div>

        <div class="subheading font-weight-regular">
          We want to add/remove travel budgets

          <div class="py-3">
            Open the following files:
            <br />
            <code>/src/components/Task4.vue</code> <br />
            <code>/src/components/BudgetRow.vue</code> <br />
            and modify the code so that:
            <ol class="list-center">
              <li>
                The <v-icon color="primary">mdi-minus-circle</v-icon> button is
                vertically aligned.
              </li>
              <li>
                When a budget type is selected and or an amount entered, the
                total budget is updated.
              </li>
              <li>
                When the <v-icon color="primary">mdi-plus-circle</v-icon> button
                is pressed, it adds another BudgetRow.
              </li>
              <li>
                When the
                <v-icon color="primary">mdi-minus-circle</v-icon> button is
                pressed, it removes that specific BudgetRow and updates the
                total budget.
              </li>
            </ol>
            Once completed, proceed to the next task.
          </div>
          <div class="text-caption">
            Note: feel free to edit any of the component properties (data,
            methods, etc..), css
          </div>
        </div>
      </v-col>

      <v-col cols="12">
        <!-- EDIT CODE BELOW -->
        <v-card>
          <v-card-subtitle> Total budget: ${{ totalBudgets }} </v-card-subtitle>

          <v-card-text v-for="item in rows" :key="item.id">
            <BudgetRow
              :data="item"
              @remove="remove"
              @changeTotal="changeTotal"
            />
          </v-card-text>

          <v-card-actions>
            <v-spacer />
            <v-btn fab dark small color="primary" @click="add">
              <v-icon>mdi-plus</v-icon>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import BudgetRow from "./BudgetRow";

export default {
  name: "Task4",
  components: {
    BudgetRow,
  },
  data() {
    return {
      totalBudgets: 0,
      startRowIndex: 1,
      rows: [
        {
          id: 1,
          amount: 0,
        },
      ],
    };
  },
  methods: {
    add() {
      this.rows.push({
        id: ++this.startRowIndex,
        amount: 0,
      });
    },
    remove(selectedRow) {
      this.rows = this.rows.filter((item) => item.id !== selectedRow.id);
      this.calculateTotalBudgets();
    },
    changeTotal(selectedRow, amout) {
      this.rows.forEach((item) => {
        item.id === selectedRow.id ? (item.amount = amout) : null;
      });
      this.calculateTotalBudgets();
    },
    calculateTotalBudgets() {
      this.totalBudgets = this.rows.reduce((result, item) => {
        return result + Number(item.amount);
      }, 0);
    },
  },
};
</script>
