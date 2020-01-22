<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          icon="menu"
          aria-label="Menu"
        />
      </q-toolbar>
      <div class="q-px-lg q-pt-xl q-mb-md">
        <div class="text-h3">Todo</div>
        <div class="subtitle1">{{dataAtual}}</div>
      </div>
      <q-img 
        src="statics/mountains.jpg"
        class="header-image absolute-top"/>
    </q-header>

 <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="250"
        :breakpoint="600"
      >
        <q-scroll-area style="height: calc(100% - 206px); margin-top: 206px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item 
              to="/"
              exact
              clickable 
              v-ripple>
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>

              <q-item-section>
                Tasks
              </q-item-section>
            </q-item>

            <q-item 
              to="/Help"
              exact
              clickable 
              v-ripple>
              <q-item-section avatar>
                <q-icon name="help" />
              </q-item-section>

              <q-item-section>
                Help
              </q-item-section>
            </q-item>            
          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top" src="statics/mountains.jpg" style="height: 206px">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="56px" class="q-mb-sm">
              <img src="https://cdn.quasar.dev/img/boy-avatar.png">
            </q-avatar>
            <div class="text-weight-bold">Diego Andrade</div>
            <div>@diegoAndrade</div>
          </div>
        </q-img>
    </q-drawer>
    <q-page-container>
      <keepalive>
        <router-view />
      </keepalive>
    </q-page-container>
  </q-layout>
</template>

<script>
import { date } from 'quasar'

export default {
  name: 'MyLayout',

  data () {
    return {
      leftDrawerOpen: false
    }
  },
  computed: {
    dataAtual() {
      let timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd, D MMM YYYY')
    }
  }
}
</script>

<style lang="scss">
  .header-image {
    height: 100%;
    z-index: -1;
    opacity: 0.5;
    filter: grayscale(100%);
  }

</style>
