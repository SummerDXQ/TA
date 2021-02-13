<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12" class="my-4">
        <div class="text-h4 mb-3">
          Task 5
        </div>

        <div class="subheading font-weight-regular">
          We want to create a trip list page

          <div class="py-3">
            You have been given the following wireframe:
          </div>

          <div>
            <img src="../assets/wireframe.png" width="600px" />
          </div>

          <div class="py-3">
            Open the file <code>/src/components/Task5.vue</code> and using the
            Vuetify library components <code>v-data-table</code> and any other
            relevant components, implement the wireframe.
          </div>

          <div>
            Feel free to diverge from the wireframe's look as needed, as long as
            the relevant information is displayed and it makes sense from a
            UI/UX perspective.
          </div>

          <div class="text-caption">
            Note: feel free to add any additional needed components and use
            <code>trips</code> to get a list of dummy trips.
          </div>
        </div>
      </v-col>

      <v-col cols="12">
        <v-card>
          <v-card-text>
            <!-- EDIT CODE BELOW -->
            <v-data-table
              :headers="headers"
              hide-default-footer
              :items="trips"
              @click:row="showDetails"
            >
              <!-- eslint-disable -->
              <template v-slot:item.destinations="{ item }">
                <span
                  v-for="(subItem, index) in item.destinations"
                  :key="subItem.location"
                >
                  {{ subItem.location.split(",")[0] }}
                  <span v-if="index !== item.destinations.length - 1">,</span>
                </span>
              </template>
              <template v-slot:item.status="{ item }">
                <span :style="{ color: color(item.status) }">
                  {{ item.status }}
                </span>
              </template>
            </v-data-table>
          </v-card-text>
        </v-card>
      </v-col>
      <div class="text-center" v-if="this.selectedRow">
        <v-dialog v-model="showDialog" width="500">
          <v-card>
            <v-card-title class="headline grey lighten-2">
              Trip Detail
            </v-card-title>
            <v-card-text class="detail">
              <div class="detail_row">
                <div>Status</div>
                <div :style="{ color: color(selectedRow.status) }">
                  {{ selectedRow.status }}
                </div>
              </div>
              <div class="detail_row">
                <div>Name</div>
                <div>{{ selectedRow.name }}</div>
              </div>
              <div class="detail_row">
                <div>Travellers</div>
                <div>{{ selectedRow.travellers.toString() }}</div>
              </div>
              <div v-if="selectedRow.destinations" class="detail_row">
                <div>Destination</div>
                <div class="destination">
                  <div v-for="item in selectedRow.destinations" :key="item.id">
                    <span class="city">{{ item.location.split(",")[0] }}</span>
                    <span>{{ item.start }}</span> to <span>{{ item.end }}</span>
                  </div>
                </div>
              </div>
            </v-card-text>

            <v-divider></v-divider>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="primary" text @click="showDialog = false">
                close
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </div>
    </v-row>
  </v-container>
</template>

<script>
import { loadTrips } from "../mock.js";

export default {
  name: "Task5",
  components: {},
  data() {
    return {
      trips: loadTrips(),
      headers: [
        {
          text: "ID",
          value: "id",
        },
        {
          text: "Name",
          value: "name",
        },
        {
          text: "Travellers",
          value: "travellers",
        },
        {
          text: "Destinations",
          value: "destinations",
        },
        {
          text: "Status",
          value: "status",
        },
      ],
      selectedRow: null,
      showDialog: false,
    };
  },
  methods: {
    showDetails(data) {
      this.selectedRow = data;
      this.showDialog = true;
    },
    color(status) {
      switch (status) {
        case "Approved":
          return "#A7DB76";
        case "Pending":
          return "#5CDCE1";
        case "Declined":
          return "#FAAD9F";
        case "Cancelled":
          return "#ffda00";
        default:
          return "#ccc";
      }
    },
  },
};
</script>

<style scoped>
.detail {
  padding: 10px 50px !important;
}
.detail_row {
  display: flex;
  margin: 10px 0;
}
.detail_row > div:first-child {
  width: 30%;
}
.detail_row > div:last-child {
  width: 70%;
}
.destination .city {
  display: inline-block;
  width: 25%;
}
</style>
