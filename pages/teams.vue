<template>
  <v-card class="mx-auto" max-width="400">
    <v-card dark flat>
      <v-card-title class="pa-2 blue lighten-1">
        <h3 class="title font-weight-light text-xs-center grow">グループ</h3>
      </v-card-title>
      <v-img
        src="grilling-2491123_640.jpg"
        gradient="to top, rgba(0,0,0,.44), rgba(0,0,0,.0)"
        aspect-ratio="1"
        max-height="150"
      >
        <template v-slot:placeholder>
          <v-row class="fill-height ma-0" align="center" justify="center">
            <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
          </v-row>
        </template>
        <v-container fill-height>
          <v-btn fab bottom right small @click="prev" color="black">
            <v-icon>chevron_left</v-icon>
          </v-btn>
          <v-layout align-center>
            <v-layout column align-center>
              <div class="headline font-weight-light">{{teamName.name}}</div>
              <!-- <v-icon large>smoke_free</v-icon> -->
            </v-layout>
          </v-layout>
          <v-btn fab bottom right small @click="next" color="black">
            <v-icon>chevron_right</v-icon>
          </v-btn>
        </v-container>
      </v-img>
    </v-card>
    <v-card-text class="py-0">
      <v-list dense>
        <v-list-item v-for="(item, index) in team" :key="index">
          <v-list-item-content>
            <v-list-item-title v-text="item.name"></v-list-item-title>
            <v-list-item-subtitle v-text="item.role"></v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-card-text>
  </v-card>
</template>

<script>
const moment = require("moment");
export default {
  components: {},
  computed: {
    teamName: {
      get() {
        return this.idxs[this.idx];
      }
    },
    team: {
      get() {
        return this.teams[this.idx];
      }
    }
  },
  data() {
    return {
      idx: 0,
      idxs: [
        { name: "テーブルA", place: "" },
        { name: "テーブルB", place: "" },
        { name: "テーブルC", place: "" }
      ],
      teams: [
        [
          {
            name: "メンバー1",
            role: "役割"
          },
          {
            name: "メンバー2",
            role: "役割"
          },
          {
            name: "メンバー3",
            role: "役割"
          },
          {
            name: "メンバー4",
            role: "役割"
          }
        ],
        [
                    {
            name: "メンバー1",
            role: "役割"
          },
          {
            name: "メンバー2",
            role: "役割"
          },
          {
            name: "メンバー3",
            role: "役割"
          },
          {
            name: "メンバー4",
            role: "役割"
          }
        ],
        [
          {
            name: "メンバー1",
            role: "役割"
          },
          {
            name: "メンバー2",
            role: "役割"
          },
          {
            name: "メンバー3",
            role: "役割"
          },
          {
            name: "メンバー4",
            role: "役割"
          }
        ]
      ]
    };
  },
  methods: {
    cvt(str) {
      return moment(str).format("HH:mm");
    },
    month(str) {
      return moment(str).format("MMMM");
    },
    dayOfMonth(str) {
      return moment(str).format("DD");
    },
    year(str) {
      return moment(str).format("YYYY");
    },
    dayOfWeek(str) {
      return moment(str).format("dddd");
    },
    next() {
      if (this.idxs.length - 1 == this.idx) {
        this.idx = 0;
      } else {
        this.idx++;
      }
    },
    prev() {
      if (0 == this.idx) {
        this.idx = this.idxs.length - 1;
      } else {
        this.idx--;
      }
    }
  }
};
</script>





