<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12" class="my-4">
        <div class="text-h4 mb-3">
          Task 2
        </div>

        <div class="subheading font-weight-regular">
          We want to build a form to record user details.

          <div class="py-3">
            Open the file <code>/src/components/Task2.vue</code> and modify the
            code below so that:
            <ol class="list-center">
              <li>
                When I press on "save", the user information is saved and the
                form is cleared.
              </li>
              <li>
                Any saved user is displayed on the right hand side table.
              </li>
            </ol>
            Once completed, proceed to the next task.
          </div>
          <div class="text-caption">
            Note: feel free to edit any of the component properties (data,
            methods, etc..)
          </div>
        </div>
      </v-col>
    </v-row>

    <!-- EDIT CODE BELOW -->
    <v-row>
      <v-col cols="12" sm="6">
        <v-card class="pa-4">
          <v-text-field label="First Name" v-model="firstName" />
          <v-text-field label="Last Name" v-model="lastName" />
          <v-btn color="primary" @click="save">Save</v-btn>
        </v-card>
      </v-col>
      <v-col cols="12" sm="6">
        <v-data-table
          :headers="[
            { text: 'First Name', value: 'firstName' },
            { text: 'Last Name', value: 'lastName' },
          ]"
          hide-default-footer
          :items="savedUsers"
        />
      </v-col>
    </v-row>
    <v-alert
      dense
      outlined
      type="error"
      v-model="showError"
      dismissible
      text
      transition="scale-transition"
      class="mt-3"
    >
      {{ errorText }}
    </v-alert>
  </v-container>
</template>

<script>
export default {
  name: "Task2",
  data() {
    return {
      firstName: "",
      lastName: "",
      savedUsers: [],
      showError: false,
      errorText: "",
    };
  },
  methods: {
    save() {
      if (!this.firstName) {
        this.showError = true;
        this.errorText = "First name is required!";
        return;
      } else if (!this.lastName) {
        this.showError = true;
        this.errorText = "Last name is required!";
        return;
      }
      this.warning = false;
      let temp = {};
      temp.firstName = this.firstName;
      temp.lastName = this.lastName;
      this.savedUsers.push(temp);
      this.firstName = "";
      this.lastName = "";
    },
  },
};
</script>
