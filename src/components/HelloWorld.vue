<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="200"
        />
      </v-col>

      <v-col class="mb-4">
        <vue-daum-map
                :appKey="appKey"
                :center.sync="center"
                :level.sync="level"
                :mapTypeId="mapTypeId"
                :libraries="libraries"
                @load="onLoad"
                @center_changed="onMapEvent('center_changed', $event)"
                @zoom_start="onMapEvent('zoom_start', $event)"
                @zoom_changed="onMapEvent('zoom_changed', $event)"
                @bounds_changed="onMapEvent('bounds_changed', $event)"
                @click="onMapEvent('click', $event)"
                @dblclick="onMapEvent('dblclick', $event)"
                @rightclick="onMapEvent('rightclick', $event)"
                @mousemove="onMapEvent('mousemove', $event)"
                @dragstart="onMapEvent('dragstart', $event)"
                @drag="onMapEvent('drag', $event)"
                @dragend="onMapEvent('dragend', $event)"
                @idle="onMapEvent('idle', $event)"
                @tilesloaded="onMapEvent('tilesloaded', $event)"
                @maptypeid_changed="onMapEvent('maptypeid_changed', $event)"
                style="width:100%;height:400px;"/>
        <h1 class="display-2 font-weight-bold mb-3">
          Welcome to Vuetify
        </h1>

        <p class="subheading font-weight-regular">
          For help and collaboration with other Vuetify developers,
          <br>please join our online
          <a
            href="https://community.vuetifyjs.com"
            target="_blank"
          >Discord Community</a>
        </p>
      </v-col>

      <v-col
        class="mb-5"
        cols="12"
      >
        <h2 class="headline font-weight-bold mb-3">
          What's next?
        </h2>

        <v-row justify="center">
          <a
            v-for="(next, i) in whatsNext"
            :key="i"
            :href="next.href"
            class="subheading mx-3"
            target="_blank"
          >
            {{ next.text }}
          </a>
        </v-row>
      </v-col>

      <v-col
        class="mb-5"
        cols="12"
      >
        <h2 class="headline font-weight-bold mb-3">
          Important Links
        </h2>

        <v-row justify="center">
          <a
            v-for="(link, i) in importantLinks"
            :key="i"
            :href="link.href"
            class="subheading mx-3"
            target="_blank"
          >
            {{ link.text }}
          </a>
        </v-row>
      </v-col>

      <v-col
        class="mb-5"
        cols="12"
      >
        <h2 class="headline font-weight-bold mb-3">
          Ecosystem
        </h2>

        <v-row justify="center">
          <a
            v-for="(eco, i) in ecosystem"
            :key="i"
            :href="eco.href"
            class="subheading mx-3"
            target="_blank"
          >
            {{ eco.text }}
          </a>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  import VueDaumMap from 'vue-daum-map';
  import config from '../config';

  export default {
    name: 'HelloWorld',
    components: {VueDaumMap},

    data: () => ({
      ecosystem: [
        {
          text: 'vuetify-loader',
          href: 'https://github.com/vuetifyjs/vuetify-loader',
        },
        {
          text: 'github',
          href: 'https://github.com/vuetifyjs/vuetify',
        },
        {
          text: 'awesome-vuetify',
          href: 'https://github.com/vuetifyjs/awesome-vuetify',
        },
      ],
      importantLinks: [
        {
          text: 'Documentation',
          href: 'https://vuetifyjs.com',
        },
        {
          text: 'Chat',
          href: 'https://community.vuetifyjs.com',
        },
        {
          text: 'Made with Vuetify',
          href: 'https://madewithvuejs.com/vuetify',
        },
        {
          text: 'Twitter',
          href: 'https://twitter.com/vuetifyjs',
        },
        {
          text: 'Articles',
          href: 'https://medium.com/vuetify',
        },
      ],
      whatsNext: [
        {
          text: 'Explore components',
          href: 'https://vuetifyjs.com/components/api-explorer',
        },
        {
          text: 'Select a layout',
          href: 'https://vuetifyjs.com/layout/pre-defined',
        },
        {
          text: 'Frequently Asked Questions',
          href: 'https://vuetifyjs.com/getting-started/frequently-asked-questions',
        },
      ],
      appKey: config.appKey, // 테스트용 appkey
      center: {lat:33.450701, lng:126.570667}, // 지도의 중심 좌표
      level: 3, // 지도의 레벨(확대, 축소 정도),
      mapTypeId: VueDaumMap.MapTypeId.NORMAL, // 맵 타입
      libraries: [], // 추가로 불러올 라이브러리
      mapObject: null // 지도 객체. 지도가 로드되면 할당됨.
    }),

    methods: {
      // 지도가 로드 완료되면 load 이벤트 발생
      onLoad (map) {
        // 지도의 현재 영역을 얻어옵니다
        var bounds = map.getBounds();
        // 영역정보를 문자열로 얻어옵니다. ((남,서), (북,동)) 형식입니다
        var boundsStr = bounds.toString();
        console.log('Daum Map Loaded', boundsStr);
        this.mapObject = map;
      },
      onMapEvent (event, params) {
        console.log(`Daum Map Event(${event})`, params);
      }
    }
  }
</script>
