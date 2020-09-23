<template>
  <v-card class="mx-auto" max-width="400">
    <v-card dark flat class="mb-2">
      <v-card-title class="pa-2 blue lighten-3">
        <h3 class="title font-weight-light text-xs-center black--text grow">{{plan}}</h3>
      </v-card-title>
      <v-img
        src="b.png"
        min-height="200"
        gradient="to top, rgba(0,0,0,.44), rgba(0,0,0,.11)"
      >
        <template v-slot:placeholder>
          <v-row class="fill-height ma-0" align="center" justify="center">
            <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
          </v-row>
        </template>

        <v-container fill-height>
          <v-layout align-center>
            <strong
              class="display-2 font-weight-regular mr-4"
            >{{dayOfMonth(day)}}-{{dayOfMonth(day2)}}</strong>
            <v-layout column justify-start>
              <div class="text-uppercase font-weight-light">{{month(day)}} {{year(day)}}</div>
              <div class="headline font-weight-light">{{dayOfWeek(day)}}-{{dayOfWeek(day2)}}</div>
            </v-layout>
          </v-layout>
        </v-container>
      </v-img>
    </v-card>

    <v-card flat class="mb-2">
      <v-card-title class="pa-2 lime lighten-2">
        <h3 class="title font-weight-light text-xs-center text-green grow">準備するもの</h3>
      </v-card-title>
      <v-img src="a.png" gradient="to top, rgba(0,0,0,.44), rgba(0,0,0,.11)">
        <template v-slot:placeholder>
          <v-row class="fill-height ma-0" align="center" justify="center">
            <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
          </v-row>
        </template>
      </v-img>
      <v-list>
        <v-list-item v-for="(item, i) in items" :key="i">
          <v-list-item-content>
            <v-list-item-title v-html="item.name"></v-list-item-title>
            <v-list-item-subtitle v-html="item.subtitle"></v-list-item-subtitle>
            <v-alert
              v-if="item.warn"
              border="left"
              type="error"
              elevation="3"
              outlined
              v-html="item.warn"
            ></v-alert>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-card>

    <v-card flat class="mb-2">
      <v-card-title class="pa-2 blue lighten-4">
        <h3 class="title font-weight-light text-xs-center text-green grow">集合時間</h3>
      </v-card-title>
      <v-list>
        <v-list-item v-for="(item, i) in meeting" :key="i">
          <v-list-item-content>
            <v-list-item-title v-html="item.time"></v-list-item-title>
            <v-list-item-subtitle v-html="item.place"></v-list-item-subtitle>
            <v-list-item-action-text v-html="item.link"></v-list-item-action-text>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-card>

    <v-card flat class="mb-2">
      <v-card-title class="pa-2 deep-orange lighten-4">
        <h3 class="title font-weight-light text-xs-center text-green grow">緊急連絡先</h3>
      </v-card-title>
      <v-list>
        <v-list-item v-for="(item, i) in emergency" :key="i">
          <v-list-item-content>
            <v-list-item-title v-html="item.name"></v-list-item-title>
            <v-list-item-subtitle><a v-bind:href="'tel:' + item.phone" v-text="item.phone"></a></v-list-item-subtitle>
            <!-- <v-list-item-action-text v-html="item.link"></v-list-item-action-text> -->
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-card>
  </v-card>
</template>

<script>
const moment = require("moment");
export default {
  components: {
  },
  data() {
    return {
      plan: "旅のプラン名称",
      day: "2020-01-01",
      day2: "2020-01-03",
      items: [
        {
          name: "必要なもの1",
          subtitle: "必要なもの 補足事項",
          warn:
            "注意事項を記載する"
        },
        {
          name: "必要なもの2",
          subtitle: "必要なもの 補足事項",
          warn:
            "注意事項を記載する"
        },
        {
          name: "必要なもの3",
          subtitle: "必要なもの 補足事項",
          warn:
            "注意事項を記載する"
        },
      ],
      meeting: [
        { place: "待ち合わせ場所A", time: "8:40" },
        {
          place:
            "<a href='https://goo.gl/maps/GUG6txJpdrw5V7hL7' target='_new'>待ち合わせ場所B</a>",
          time: "9:00"
        }
      ],
      emergency: [
        { name: "担当者A", phone: "XXXXXXXXXXX" },
        { name: "担当者B", phone: "XXXXXXXXXXX" }
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
    }
  }
};
</script>
