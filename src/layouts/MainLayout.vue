<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
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
        <div class="text-h3">Todo</div>
        <div class="text-subtitle1">{{ todaysDate }}</div>
      </div>
      <q-img
        src="mountains.jpg"
        class="header-image absolute-top"
      />
    </q-header>

    <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="250"
        :breakpoint="600"
      >
        <q-scroll-area style="height: calc(100% - 192px); margin-top: 192px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item
              to="/"
              clickable
              v-ripple>
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>

              <q-item-section>
                Todo
              </q-item-section>
            </q-item>

            <q-item
              to="/help"
              clickable
              v-ripple>
              <q-item-section avatar>
                <q-icon name="help" />
              </q-item-section>

              <q-item-section>
                Ajuda
              </q-item-section>
            </q-item>
          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top" src="mountains.jpg" style="height: 192px">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="56px" class="q-mb-sm">
              <img src="https://media-exp1.licdn.com/dms/image/C5603AQHiLLKenhFfkg/profile-displayphoto-shrink_800_800/0/1619818640363?e=1631145600&v=beta&t=Aw4WZYI61RNp4yPf571gfVCdDkAcNNvDOqj8AHE1cPQ">
            </q-avatar>
            <div class="text-weight-bold">Marcelo Rocha Ferreira</div>
            <div>@marcelorocfer</div>
          </div>
        </q-img>
      </q-drawer>

    <q-page-container>
      <router-view v-slot="{ Component }">
      <keep-alive>
        <component :is="Component" />
      </keep-alive>
    </router-view>
    </q-page-container>
  </q-layout>
</template>

<script>
import { date } from 'quasar'

import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'MainLayout',

  computed: {
    todaysDate() {
      let timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd D MMMM')
    }
  },

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>

<style lang="scss">
  .header-image {
    height: 100%;
    z-index: -1;
    opacity: 0.5;
    filter: grayscale(100%);
  }
</style>
