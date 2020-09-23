<template>
  <v-card class="mx-auto" max-width="400">
    <v-card flat>
      <v-card-title class="pa-2 blue lighten-1">
        <h3 class="title font-weight-light text-xs-center grow">部屋割り</h3>
      </v-card-title>
      <v-sheet :color="roomName.color" height="150" tile>
        <v-container fill-height>
          <v-btn fab bottom right small @click="prev">
            <v-icon>chevron_left</v-icon>
          </v-btn>
          <v-layout align-center>
            <v-layout column align-center>
              <div class="headline font-weight-light">{{roomName.name}}</div>
              <v-icon large v-if="roomName.smoke">smoking_rooms</v-icon>
              <v-icon large v-else>smoke_free</v-icon>
            </v-layout>
          </v-layout>
          <v-btn fab bottom right small @click="next">
            <v-icon>chevron_right</v-icon>
          </v-btn>
        </v-container>
      </v-sheet>
    </v-card>
    <v-card-text class="py-0">
      <v-list dense>
        <v-list-item v-for="(item, index) in room" :key="index">
          <v-list-item-content>
            <v-list-item-title v-text="item.name"></v-list-item-title>
          </v-list-item-content>
          <v-list-item-action>
            <v-icon v-if="item.f" color="pink lighten-1">info</v-icon>
            <v-icon v-if="item.o" color="blue lighten-1">grade</v-icon>
          </v-list-item-action>
        </v-list-item>
      </v-list>
    </v-card-text>
  </v-card>
</template>

<script>
const moment = require("moment");
export default {
  components: {
  },
  computed: {
    roomName: {
      get() {
        return this.idxs[this.idx];
      }
    },
    room: {
      get() {
        return this.member[this.idx];
      }
    }
  },
  data() {
    return {
      idx: 0,
      idxs: [
        { name: "コテージA", smoke: false, color: "light-blue lighten-3" },
        { name: "コテージB", smoke: true, color: "teal lighten-3" },
        { name: "コテージC", smoke: false, color: "green lighten-3" },
        { name: "コテージD", smoke: false, color: "orange lighten-3" }
      ],
      images: {
        "2019-09-27": "a.png",
        "2019-09-28": "b.png"
      },
      member: [
        [
          {
            name: "メンバー1"
          },
          {
            name: "メンバー2"
          },
          {
            name: "メンバー3"
          },
          {
            name: "メンバー4"
          },
          {
            name: "メンバー5",
            o: true //
          }
        ],
        [
          {
            name: "メンバー1"
          },
          {
            name: "メンバー2"
          },
          {
            name: "メンバー3"
          },
          {
            name: "メンバー4"
          },
          {
            name: "メンバー5",
            o: true //
          }
        ],
        [
          {
            name: "メンバー1"
          },
          {
            name: "メンバー2"
          },
          {
            name: "メンバー3"
          },
          {
            name: "メンバー4"
          },
          {
            name: "メンバー5",
            o: true //
          }
        ],
        [
          {
            name: "メンバー1",
            f:true
          },
          {
            name: "メンバー2",
            f:true
          },
          {
            name: "メンバー3",
            f:true
          },
          {
            name: "メンバー4",
            f:true
          },
          {
            name: "メンバー5",
            f:true,
            o: true //
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





