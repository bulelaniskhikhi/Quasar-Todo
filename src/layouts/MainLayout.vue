<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated style="background-color: #f5f5f5; color: black">
      <q-toolbar >
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />
        
      </q-toolbar>
      <div class="q-px-lg q-pt-xl q-mb-md">
        <div class="text-h3">
          Todo
        </div>
        <div class="text-subtitle">
          {{todaysDate}}
        </div>
      </div>
      <!-- <q-img src="../../public/images/simone-hutsch-XK0faa4_mCQ-unsplash.jpg" 
      class="header-image absolute-top"/> -->
      
    </q-header>

    <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="300"
        :breakpoint="600"
      >
        <q-scroll-area style="height: calc(100% - 187px); margin-top: 187px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item 
            to="/"
            clickable 
            v-ripple
            
            >
              <q-item-section avatar style="color:black">
                <q-icon name="list" />
              </q-item-section>

              <q-item-section
              style="color:black;">
                To Do
              </q-item-section>
            </q-item>

            <q-item 
            to="/help"
            clickable 
            v-ripple>
              <q-item-section avatar style="color:black;">
                <q-icon name="help" />
              </q-item-section>

              <q-item-section style="color:black">
                Help
              </q-item-section>
            </q-item>

          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top"  style="height: 187px; background-color: #E0E0E0;">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="66px" class="q-mb-sm">
              <img src="https://i.postimg.cc/hPHBtQ1Z/DOD2-Manah-CGI6.jpg">
            </q-avatar>
            <div style="color:black" class="text-weight-bold">Xena Vermont</div>
            <div style="color:black">@succubus.at.work</div>
          </div>
        </q-img>
      </q-drawer>

    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>

<script>
import { date } from 'quasar'


import { defineComponent, ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'

const linksList = [
  {
    title: 'Docs',
    caption: 'quasar.dev',
    icon: 'school',
    link: 'https://quasar.dev'
  },
  {
    title: 'Github',
    caption: 'github.com/quasarframework',
    icon: 'code',
    link: 'https://github.com/quasarframework'
  },
  {
    title: 'Discord Chat Channel',
    caption: 'chat.quasar.dev',
    icon: 'chat',
    link: 'https://chat.quasar.dev'
  },
  {
    title: 'Forum',
    caption: 'forum.quasar.dev',
    icon: 'record_voice_over',
    link: 'https://forum.quasar.dev'
  },
  {
    title: 'Twitter',
    caption: '@quasarframework',
    icon: 'rss_feed',
    link: 'https://twitter.quasar.dev'
  },
  {
    title: 'Facebook',
    caption: '@QuasarFramework',
    icon: 'public',
    link: 'https://facebook.quasar.dev'
  },
  {
    title: 'Quasar Awesome',
    caption: 'Community Quasar projects',
    icon: 'favorite',
    link: 'https://awesome.quasar.dev'
  }
]

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink
  },

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  },

  computed: {
    todaysDate(){
      const timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd DD MMMM YYYY')
    }
  }
})
</script>

<style scoped>
.header-image {
  height: 100%;
  z-index: -1;
  opacity: 0.2;
  filter: grayscale(100%)
}
</style>
