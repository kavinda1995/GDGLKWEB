<template>
  <v-toolbar
    app
    color="white"
    height="55px"
    scroll-off-screen
  >
    <v-toolbar-side-icon
      class="hidden-md-and-up"
      @click="toggleDrawer"

    />

    <v-toolbar-title class="ml-0 pl-1 mr-1">
      <span class="google-font">{{ChapterDetails.ChapterName}}</span>
    </v-toolbar-title>
    <v-spacer />
    <v-btn
        v-for="(link, i) in links"
        :key="i"
        :to="link.to"
        class="ml-0 google-font hidden-sm-and-down"
        style="text-transform: capitalize;" 
        flat
        @click="onClick($event, link)"
      >
        {{ link.text }}
    </v-btn>
    <v-flex xs1>
      <v-layout
              align-center
              justify-center
      >
        <img
                src="@/assets/img/notification.png"
                style="width: 36px; height: 36px;"
                alt="Notification_icon"/>
      </v-layout>

    </v-flex>

  
  </v-toolbar>
</template>

<script>
import ChapterDetails from '@/assets/data/chapterDetails.json'
  // Utilities
  import {
    mapGetters,
    mapMutations
  } from 'vuex'
  export default {
    data() {
      return {
        ChapterDetails:ChapterDetails
      }
    },
    computed: {
      ...mapGetters(['links'])
    },
    methods: {
      ...mapMutations(['toggleDrawer']),
      onClick (e, item) {
        e.stopPropagation()
        if (item.to || !item.href) return
        this.$vuetify.goTo(item.href)
      }
    }
  }
</script>
