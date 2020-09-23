<template>
  <v-card class="mx-auto" max-width="400">
    <v-card dark flat>
      <v-card-title class="pa-2 green lighten-1">
        <h3 class="title font-weight-light text-xs-center grow">タイムライン</h3>
      </v-card-title>
      <v-img
        :src="cover"
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
          <v-btn fab bottom right small @click="prev">
            <v-icon>chevron_left</v-icon>
          </v-btn>
          <v-layout align-center>
            <strong class="display-4 font-weight-regular mr-4">{{dayOfMonth(day)}}</strong>
            <v-layout column justify-end>
              <div class="headline font-weight-light">{{dayOfWeek(day)}}</div>
              <div class="text-uppercase font-weight-light">{{month(day)}} {{year(day)}}</div>
            </v-layout>
          </v-layout>
          <v-btn fab bottom right small @click="next">
            <v-icon>chevron_right</v-icon>
          </v-btn>
        </v-container>
      </v-img>
    </v-card>
    <v-card-text class="py-0">
      <v-timeline align-top dense>
        <v-timeline-item
          v-for="(item, index) in schedule"
          :key="index"
          :color="item.c"
          fill-dot
          :hide-dot="item.t?false:true"
          :icon="item.t?'':'info'"
          right
        >
          <v-card :color="item.c">
            <v-card-title>
              <span v-if="item.t" class="body-2 pr-3" v-text="cvt(item.t)"></span>
              <span class="body-2" v-html="item.s"></span>
            </v-card-title>
            <v-card-text v-if="item.d" class="white text--primary">
              <v-container>
                <v-layout pt-3>
                  <v-flex>
                    <div class="caption" v-html="item.d"></div>
                  </v-flex>
                </v-layout>
              </v-container>
            </v-card-text>
          </v-card>
        </v-timeline-item>
      </v-timeline>
    </v-card-text>
  </v-card>
</template>

<script>
const moment = require("moment");
export default {
  components: {
  },
  computed: {
    schedule: {
      get() {
        return this.schedules[this.day];
      }
    },
    cover: {
      get() {
        return this.images[this.day];
      }
    }
  },
  data() {
    return {
      day: "2020-01-01",
      days: ["2020-01-01", "2020-01-02"],
      images: {
        "2020-01-01": "a.png",
        "2020-01-02": "b.png"
      },
      schedules: {
        "2020-01-01": [
          {
            t: "2020-01-01 08:40",
            c: "blue",
            s: "集合時間"
          },
          {
            t: "2020-01-01 09:00",
            c: "yellow",
            s: "出発"
          },
          {
            t: "2020-01-01 09:00",
            c: "blue",
            s: "駅前集合時間",
            d:
              ""
          },
          {
            t: "2020-01-01 09:10",
            c: "yellow",
            s: "駅前出発"
          },
          {
            c: "deep-purple lighten-4",
            s: "バス移動中"
          },
          {
            t: "2020-01-01 09:45",
            c: "yellow",
            s: "Sample",
            d: ""
          },
          {
            t: "2020-01-01 10:40",
            c: "yellow",
            s: "Sample出発"
          },
          {
            c: "deep-purple lighten-4",
            s: "バス移動中"
          },
          {
            t: "2020-01-01 10:50",
            c: "yellow",
            s: "酒造",
            d: "日本酒メーカー"
          },
          {
            c: "deep-purple lighten-4",
            s: "バス移動中"
          },
          {
            t: "2020-01-01 11:50",
            c: "yellow",
            s: "食事処",
            d: "食事"
          },
          {
            c: "deep-purple lighten-4",
            s: "バス移動中"
          },
          {
            t: "2020-01-01 12:50",
            c: "yellow",
            s: "目的地A到着"
          },
          {
            t: "2020-01-01 14:40",
            c: "yellow",
            s: "目的地B到着",
            d: ""
          },
          {
            t: "2020-01-01 15:00",
            c: "light-green",
            s: "目的地C到着"
          },
          {
            c: "pink",
            s: "自由時間",
            d: ""
          },
          {
            t: "2020-01-01 16:30",
            c: "red accent-2",
            s: "BBQ準備開始",
            d: "グループに別れて<br>BBQを行います。"
          },
          {
            t: "2020-01-01 17:00",
            c: "red accent-4",
            s: "BBQ開始",
            d: "グループに分かれて、BBQの準備をします。<br>役割は、<a href='/teams'>グループ</a>で確認。"
          },
          {
            t: "2020-01-01 17:29",
            c: "brown accent-4",
            s: "日没"
          },
          {
            t: "2020-01-01 19:00",
            c: "light-blue",
            s: "後片付け"
          },
          {
            t: "2020-01-01 20:00",
            c: "pink",
            s: "温泉",
            d: "いい湯だな"
          },
          {
            c: "pink",
            s: "自由時間",
            l: "/rooms"
          },
          {
            t: "2020-01-01 22:00",
            c: "brown darken-4 white--text",
            s: "就寝時間",
            d: "22時以降は、屋外での活動はお控えください。<br>"
          }
        ],
        "2020-01-02": [
          {
            t: "2020-01-02 07:00",
            c: "yellow",
            s: "起床時間"
          },
          {
            t: "2020-01-02 07:00",
            c: "lime lighten-4",
            s: "朝食",
            d: "サンドイッチ/御飯etc"
          },
          {
            t: "2020-01-02 09:00",
            c: "yellow",
            s: "ごみ捨て/移動準備",
            d: ""
          },
          {
            t: "2020-01-02 09:45",
            c: "blue",
            s: "バスに集合",
            d: "10:00までにバスに集合してください。"
          },
          {
            c: "deep-purple lighten-4",
            s: "バス移動中"
          },
          {
            t: "2020-01-02 10:35",
            c: "yellow",
            s: "サービスエリア",
            d: "いろいろあるよ"
          },
          {
            c: "deep-purple lighten-4",
            s: "バス移動中"
          },
          {
            t: "2020-01-02 11:40",
            c: "blue lighten-3",
            s: "駅西口"
          }
        ]
      }
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
      this.day = this.days[1];
    },
    prev() {
      this.day = this.days[0];
    }
  }
};
</script>
